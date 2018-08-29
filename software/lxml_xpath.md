xpath语法

```python
from lxml import etree

doc=etree.HTML(text)
for div in doc.xpath("//div[@class='category-item m']"):
    l1_class = div.xpath("div[@class='mt']/h2[@class='item-title']/span/text()")[0]
    for dl in div.xpath("div[@class='mc']/div[@class='items']/dl"):
        
        l2_class_url = dl.xpath("dt/a/@href")[0]
        l2_class = dl.xpath("dt/a/text()")[0]
        print(l1_class, l2_class, l2_class_url)
        
        for a in dl.xpath('dd/a'):
            name = a.xpath('text()')[0]
            url = a.xpath('@href')[0]
            print(name, url)
```