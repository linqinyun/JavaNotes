# XML
- 可拓展标记语言
- XML 以文件形式保存数据，没有预置的标签，标签自己定义  
  XML重在保存与传输数据，HTML用于显示信息
- 用途：
  1. Java程序中XML作为配置描述文件
  2. 用于保存程序产生的数据（XML是非常好的数据载体）
  3. 网络间的数据传输
## XML文档结构
- XML文档结构
  1. 第一行必须是XML声明
  2. 对于整个文档来说只能有且只有一个根节点
  3. XML标签书写规则与HTML相同
- XML声明
> XML声明说明XML文档的基本信息，包括本号与字符集，在XML第一行。  
```
<?xml version="1.0" encoding="utf-8"?>
      版本号1.0/1.1  编码-字符集utf-8
```
- 一.合法的标签名
  1. 标签名要有意义
  2. 建议使用英文，小写字母，单词之间使用"-"分割
  3. 建议多级标签之间不要存在重名

- 二.适当的注释与缩进  
  适当的注释与缩进可以让XML文档更容易阅读

- 三.合理使用属性
  1. 标签属性用于描述标签不可或缺的信息
  2. 对标签分组或者为标签设置ID时常用属性表示。

- 四.特殊字符与CDATA标签  
  标签体中，出现"<"、">"特殊字符，会破坏文档结构。  
  解决方法1.使用实体引用。  
  ```
  &It;=<=小于  
  &gt;=>=大于  
  &amp;=&=和号  
  &apos;='=单引号  
  &quot;="=双引号  
  ```
  解决方法2.使用CDATA标签。  
  1. CDATA指的是不应由XML解析器进行解析的文本数据
  2. 从"<![CDATA["开始,到"]]>"结束

- 五.有序的子元素  
  在XML多层嵌套的子元素中，标签前后顺序因保持一致。     
## XML语义约束  
1. XML文档结构正确，但可能不是有效的。
> 例如：员工档案XML中绝不允许出现"植物品种"标签。XML语义约束就是用于规定XML文档中允许出现哪些元素。
2. XML语义约束有两种定义方式：DTD与XMLSchema。

- DTD（Document Type Definition）:DTD 是一种简单易用的语义约束方式
> DTD的文件扩展名为.dtd

- DTD定义节点：
>利用DTD中的<！ELEMENT>标签，我们可以定义XML文档中允许出现的节点以及数量
```
定义hr节点下只允许出现1个employee子节点
<!ELEMENT hr (employee)> 

<!ELEMENT hr (employee)+>至少一个

<!ELEMENT hr (employee)?>

最多一个employee节点下必须包含以下四个节点，且按顺序出现
<!ELEMENT employee (name,age,salary,department)>

定义name标签只能是文本，#PCDATA代表文本元素
<!ELEMENT name (#PCDATA)>
```
- DTD定义节点数量
1. 如某个子节点需要多次重复出现，则需要在子节点后增加相应的描述符。
```
例如：
[1]<!ELEMENT hr (employee+)>
hr节点下最少出现1个employee子节点。

[2]<!ELEMENT hr (employee*)>
hr节点下可出现0..n个employee子节点。

[3]<!ELEMENT hr (employee？)>
hr节点下最多出现1个employee子节点。
```
- XML引用DTD文件
>在XML中使用<!DOCTYPE>标签来引用DTD文件 书写格式：
```
<!DOCTYPE 根节点 SYSTEM "dtd文件路径">

实例：<!DOCTYPE hr SYSTEM "hr.dtd">    
```   
#### schema
```
XML
<?xml version="1.0" encoding="UTF-8"?>

<hr xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"  xsi:noNamespaceSchemaLocation="hr.xsd">
	<employee no="3309">
		<name>test</name>
		<age>31</age>
		<salary>4000</salary>
		<department>
			<dname>会计部</dname>
			<address>XX大厦-B103</address>
		</department>
	</employee>
	<employee no="3310"> 
		<name>test</name>
		<age>32</age>
		<salary>5000</salary>
		<department>
			<dname>信息部</dname>
			<address>XX大厦-B103</address>
		</department>
	</employee>
</hr>
```
```
schena
<?xml version="1.0" encoding="UTF-8"?>
<schema xmlns="http://www.w3.org/2001/XMLSchema">
	<element name="hr">
		<!-- 复杂节点  -->
		<complexType>
			<sequence>
				<element name="employee" minOccurs="1" maxOccurs="9999">
					<complexType>
						<sequence>
							<element name="name" type="string"></element>
							<element name="age">
								<simpleType>
									<restriction base="integer">
										<minInclusive value="18"></minInclusive>
										<maxInclusive value="76"></maxInclusive>
									</restriction>
								</simpleType>
							</element>
							<element name="salary" type="integer"></element>
							<element name="department">
								<complexType>
									<sequence>
										<element name="dname" type="string"></element>
										<element name="address" type="string"></element>
									</sequence>
								</complexType>
							</element>
						</sequence>
						<attribute name="no" type="string" use="required"></attribute>
					</complexType>
				</element>
			</sequence>
		</complexType>
	</element>
</schema>
```
#### XML提取
- Java提取XML使用dom4j这个jar包
```
package pers.java.dom4j;

import java.util.List;

import org.dom4j.Attribute;
import org.dom4j.Document;
import org.dom4j.DocumentException;
import org.dom4j.Element;
import org.dom4j.io.SAXReader;

public class HrReader {
	
	public void readHml() {
		String file ="D:\\eclipseWorkspace\\ObjectProj\\src\\pers\\java\\xml\\hr.xml";
		// 读取xml核心类
		SAXReader reader = new SAXReader();
		try {
			Document document = reader.read(file);
			//获取根节点
			Element root = document.getRootElement();
			//elements获取指定的标签合集
			List<Element> employees = root.elements("employee");
			for(Element employee:employees) {
				//element方法用于获取唯一的子节点对象
				Element name = employee.element("name");
				String empName = name.getText();
				System.out.println(empName);
				System.out.println(employee.elementText("age"));
				System.out.println(employee.elementText("salary"));
				Element department = employee.element("department");
				System.out.println(department.elementText("dname"));
				System.out.println(department.elementText("address"));
				//提取属性
				Attribute att = employee.attribute("no");
				System.out.println(att.getText());
			}
		} catch (DocumentException e) {
			// TODO Auto-generated catch block
			e.printStackTrace();
		}
	}
	public static void main(String[] args) {
		// TODO Auto-generated method stub
		HrReader hr = new HrReader();
		hr.readHml();
	}

}

```