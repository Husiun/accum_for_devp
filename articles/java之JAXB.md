															java之JAXB技术
	项目中有用到java中的JAXB技术，对其做一个比较全面的学习。个人理解JAXB技术就是提供一个标准用于java bean和xml文件的相互转换，主要依赖其强大的注解实现。
		1.概念
	JAXB(即Java Architecturefor XML Binding)是一个业界的标准，即是一项可以根据XML Schema产生java类的技术，同时也能将java对象树重新写到XML实例文档中。
		2.注解解释(annotation)
	注解主要作用于javabean，
	1）@XmlAccessorType()  用于指定由java对象生成xml文件时对java对象属性的访问方式，常与@XmlType,@XmlRootElement一起使用
	访问方式位于注解XmlAccessType里面的几个常量，XmlAccessType.FIELD java对象中的所有成员变量
	XmlAccessType.PROPERTY java对象中所有通过getter/setter方式访问的成员变量
	XmlAccessType.PUBLIC_MEMBER java对象中所有的public访问权限的成员变量和getter/setter方式访问的成员变量 XmlAccessType.NONE  java 对象中的所有属性都不映射到xml文档中
	注意：属性的访问方式默认是XmlAccessType.PUBLIC_MEMBER,当成员变量使用了XmlTransient注解的时候，就表示此变量不映射到xml文档中，不管上面设置的访问方式是哪一个，当private的属性权限提升为public的时候不需要额外加注释，已经有默认值。
	2）@XmlType 该注解作用于类上面，常与@XmlAccessorType,@XmlRootElement一起使用，它有三个属性name,namspace,propOrder,在使用propOrder属性时通常需要将所有的成员变量加上
	@XmlType(propOrder={"name","sex","age"})
	public class Test{
		private String name;
		private String sex;
		private int age;
	}
	3)@XmlRootElement 该注解用于指定java bean转换为xml文件xml的根元素，如果不指定该元素，默认跟元素与类名相同
	4)@XmlElement 该注解作用于类成员变量，用于指定需要将其映射到xml中，其中有一个name属性，可以将属性映射到对应的xml中的名字更改，否则默认为属性名
	注解@xmlAttribute与之相同
	@XmlElement(name="user_name")  ----xml中实际名字
	private String name;
	5)@xmlTransient 该注解作用于类成员变量，指定对应的元素不需要映射到xml中
	6)@XmlAccessorOrder
	用于对java对象生成的xml元素进行排序。它有两个属性值：AccessorOrder.ALPHABETICAL：对生成的xml元素按字母顺序排序；
	XmlAccessOrder.UNDEFINED：不排序。
	7)@XmlJavaTypeAdapter   @XmlJavaTypeAdapter常用在转换比较复杂的对象时，如map类型或者格式化日期等。使用此注解时，需要自己写一个adapter类继承XmlAdapter抽象类，并实现里面的方法
		3.用到的类
	主要涉及的类包括：JAXBcontext 创建context对象 
	Marshaller   将java bean 对象转换为xml   里面有setProperty方法用于对生成的xml做调整，比如编码格式，是否自动换行等
	Unmarshaller 将xml转为java bean对象  
	常用到StringWriter StringReader类，相对于java bean来说是read  
	
	