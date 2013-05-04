---
layout: post
title: A webcomic plugin for Jekyll
---

# A webcomic plugin for Jekyll

This was a short diversion to see if I could help get a simple webcomic up and
running online.  It needed to be simple to update and lightweight.
Unfortunately, all the webcomic frameworks I could find
[look](http://wordpress.org/extend/plugins/webcomic/)
[like](http://comiccms.com/)
[this](http://comicpress.org/).
WordPress isn't terrible
to set up, but it can be a bother to configure.  Jekyll sounded like a fun
way to get the project started.

As far as I could tell, no one else had done something like this, or at least
published how to do it.  The plugin needed to be able to:

* Generate an "index" of all pages of a particular comic.
* Have a direct link to the "last" page of the comic.
* Support multiple comics.

A few hours later, this was the result:

{% highlight ruby %}
module Jekyll
  class ComicPage < Page
    def initialize(site, base, comic, img_path, img_file, total)
      @site  = site
      @base  = base
      @dir   = "/comics/#{comic}"
      @comic = comic
      @page_num = File.basename(img_file, File.extname(img_file))
      @total = total
      @name = @page_num + '.html'

      puts "Generating #{@comic} page #{@page_num}"

      self.process(@name)
      self.data ||= Hash.new
      self.data['src'] = "/#{img_path.chomp('/')}/#{img_file}"
      self.data['next'] = next_page
      self.data['prev'] = prev_page
      self.data['num'] = @page_num
      self.data['last'] = last_page
      self.data['first'] = first_page

      self.read_yaml(File.join(base, '_layouts'), comic + '.html')
    end

    def next_page
      return nil if @page_num.to_i >= (@total - 1)
      return @dir + '/' + pad(@page_num.to_i + 1) + '.html'
    end

    def prev_page
      return nil if @page_num.to_i == 0
      return @dir + '/' + pad(@page_num.to_i - 1) + '.html'
    end

    def last_page
      return @dir + '/last.html'
    end

    def first_page
      return @dir + '/' + pad(0) + '.html'
    end

    def pad(i)
      width = @page_num.length
      return i.to_s.rjust(width, '0')
    end
  end

  class ComicLastPage < ComicPage
    def initialize(site, base, comic, img_path, img_file, total)
      super

      @name = 'last.html'
      self.process(@name)
    end
  end

  class ComicIndexPage < Page
    def initialize(site, base, comic, images)
      @site = site
      @base = base
      @dir = "/comics/#{comic}"
      @comic = comic
      @name = 'index.html'

      self.data ||= Hash.new
      self.data['images'] = images.collect{ |img| File.basename(img, File.extname(img)) }
      self.process(@name)
      self.read_yaml(File.join(base, '_layouts'), "#{comic}_index.html")
    end
  end


  class GenerateComics < Generator
    safe true
    priority :normal

    def generate(site)
      return unless Dir.exists?('_comics')

      Dir.glob('_comics/*.yml').each do |file|
        comic = File.basename(file, '.yml')
        config = YAML.load_file(file)
        self.write_comic(site, comic, config['images'])
      end

    end

    def write_comic(site, comic, img_path)
      images = Dir.glob("#{img_path}/*.{jpg,png,jpeg,gif,bmp}").select { |f| File.basename(f) =~ /(\d)+\.(jpg|png|jpeg|gif|bmp)/ }
      images.each do |file|
        c = ComicPage.new(site, site.source, comic, img_path, File.basename(file), images.length)
        c.render(site.layouts, site.site_payload)
        c.write(site.dest)

        site.pages << c
        site.static_files << c
      end

      l = ComicLastPage.new(site, site.source, comic, img_path, File.basename(images[-1]), images.length)
      l.render(site.layouts, site.site_payload)
      site.pages << l
      site.static_files << l

      i = ComicIndexPage.new(site, site.source, comic, images)
      i.render(site.layouts, site.site_payload)
      site.pages << i
      site.static_files << i
    end
  end
end
{% endhighlight %}

The plugin works by adding a \_comics folder, with YAML configuration files for
each comic you want to roll into the site. At this point, all it cares about is
a path to some image files.  Each ComicPage corresponds to a single image file,
which also needs to be named numerically, or at the very least, in Unix file
sort order.

A sample comic config file (let's call it 'mycomic.yml') would look like this:

{% highlight yaml %}
images: images/mycomic/
{% endhighlight %}

The generator pumps out ComicPages, one per image, organized under
/comics/.  There's probably a more efficient way to do this, but the code works
well enough for a couple hundred comic pages.  I've also made the code
available as a [GitHub Gist](https://gist.github.com/nompute/5131217).
