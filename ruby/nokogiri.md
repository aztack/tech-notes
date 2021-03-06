忽略空白符
=============
必须用Nokogiri::XML加noblanks选项。Nokogiri::HTML不行
```ruby
Nokogiri:XML(html,&:noblanks)
```

强制UTF8编码
============
```ruby
doc = Nokogiri::XML(a, nil, "UTF-8")
```

搜索文本节点
===
```ruby
doc.xpath("//text()").each{|textNode|}
```

删除空白文本节点
===

```ruby
doc.xpath("//text()").each{|e| e.remove if e.content =~ /^\s+$/}
```

格式化HTML
===

```ruby
doc = Nokogiri::HTML(html, &:noblanks)
xml = doc.to_xml(:indent => 4)

node.inner_html = xml #xml format will be messed up, use .content instead
node.content = xml
```

增加节点
========
```ruby
class ::Nokogiri::XML::Element
	def append_newline
		self.add_next_sibling self.document.create_text_node("\n")
	end

	def prepend_newline
		self.add_previous_sibling self.document.create_text_node("\n")
	end

	def append_comment(comment)
		self.add_next_sibling self.document.create_comment(comment)
	end

	def prepend_comment(comment)
		self.add_previous_sibling self.document.create_comment(comment)
	end
end
```

阻止中文被转义
====
```ruby
doc.to_html(:encoding => 'utf-8')
```
