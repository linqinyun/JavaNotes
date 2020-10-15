# 集合
## 应用场景
- 无法预测存储数据的数据
- 同时存储具有一对一关系的数据
- 需要进行数据的增删
- 数据重复问题
## 集合框架的体系结构
- Collection
  - 类的对象
  - List
    - ArrayList
  - Queue
    - LinkedList
  - Set
    - HashSet
- Map
  - 键值对
  - HashMap

### List
- List是元素有序并且可以重复的集合，称为序列
- List可以精确的控制每一个元素的插入位置，或删除某个位置的元素
- List的主要两个是实现类是ArrayList和LinkedList
#### ArrayList
- ArrayList底层是由数组是实现的
- 动态增长，以满足应用程序的需要
- 在列表尾部插入或删除数据非常有效
- 更适合查找和更新元素
- ArrayList中的元素可以为null
- 基本使用操作字符串  
```
		List list = new ArrayList();
		
		list.add("Java");
		list.add("C");
		list.add("C++");
		list.add("Go");
		list.add("swift");
		//输出
		System.out.println("元素输出：" + list.size());
		//遍历数据
		System.out.println("*************************");
		for(int i=0;i<list.size();i++) {
			System.out.print(list.get(i)+" ");
		}
		//移除列表中的C++
		System.out.println();
//		list.remove(2);
		list.remove("C++");
		System.out.println("****************");
		//移除后的
		for(int i=0;i<list.size();i++) {
			System.out.print(list.get(i)+" ");
		}
```
- 基本使用操作自定义对象
```
//公告发布/修改/删除
		Notices notices1 = new Notices(1,"欢迎来到1","管理员1",new Date());
		Notices notices2 = new Notices(2,"欢迎来到2","管理员2",new Date());
		Notices notices3 = new Notices(3,"欢迎来到3","管理员3",new Date());
		
		ArrayList noticesList = new ArrayList();
		noticesList.add(notices1);
		noticesList.add(notices2);
		noticesList.add(notices3);
		
		
		System.out.println("公告内容：");
		for(int i=0;i<noticesList.size();i++) {
			System.out.println((i+1)+":"+((Notices)(noticesList.get(i))).getTitle());
		}
		
		Notices notices4 = new Notices(4,"欢迎来到4","管理员4",new Date());
		noticesList.add(1,notices4);
		System.out.println("公告内容：");
		for(int i=0;i<noticesList.size();i++) {
			System.out.println((i+1)+":"+((Notices)(noticesList.get(i))).getTitle());
		}
		
		noticesList.remove(notices2);
		
		System.out.println("公告内容：");
		for(int i=0;i<noticesList.size();i++) {
			System.out.println((i+1)+":"+((Notices)(noticesList.get(i))).getTitle());
		}
		
		notices4.setTitle("test");
		noticesList.set(1, notices4);
		
		System.out.println("公告内容：");
		for(int i=0;i<noticesList.size();i++) {
			System.out.println((i+1)+":"+((Notices)(noticesList.get(i))).getTitle());
		}
```
#### Set
- Set是元素无序并且不可以重复的集合，并称为集
#### HashSet
- HashSet是Set的一个重要实现类，称为哈希集
- HashSet中的元素无序并且不可以重复
- HashSet中只允许一个null元素
- 具有良好的存取和查找性能
```
案例
		Cat cat1 = new Cat("小猫1",12,"白尾");
		Cat cat2 = new Cat("小猫2",8,"黑尾");
		Cat cat3 = new Cat("小猫3",7,"黄尾");
		
		Set<Cat> set = new HashSet<Cat>();
		set.add(cat1);
		set.add(cat2);
		set.add(cat3);
		
		Iterator<Cat> it = set.iterator();
		while(it.hasNext()) {
			System.out.println(it.next());
		}
		System.out.println("===================");
		System.out.println("插入重复信息");
		Cat cat4 = new Cat("小猫1",12,"白尾");
		set.add(cat4);
		it = set.iterator();
		while(it.hasNext()) {
			System.out.println(it.next());
		}
		System.out.println("===================");
		System.out.println("插入new信息");
		Cat cat5 = new Cat("小猫4",16,"灰尾");
		set.add(cat5);
		it = set.iterator();
		while(it.hasNext()) {
			System.out.println(it.next());
		}
		//查找
		System.out.println("===================");
		if(set.contains(cat1)) {
			System.out.println(cat1);
		}else {
			System.out.println("no");
		}
		System.out.println("===================");
		boolean flag = false;
		Cat c = null;
		it = set.iterator();
		while(it.hasNext()) {
			c = it.next();
			if(c.getName().equals("小猫1")) {
				flag = true;
				break;
			}
		}
		if(flag)
			System.out.println(c);
		else
			System.out.println("no");
		
		System.out.println("===================");
		
		//删除信息
//		for(Cat cat:set) {
//			if("小猫3".equals(cat.getName())) {
//				set.remove(cat);break;
//			}
//		}
		Set<Cat> st1 = new HashSet<Cat>();
		for(Cat cat:set) {
			if(cat.getMonth()<12) {
				st1.add(cat);
			}
		}
		set.removeAll(st1);
		System.out.println("delete");
		for(Cat cat:set) {
			System.out.println(cat);
		}
		
		System.out.println("===================");
		
		boolean flag1 = set.removeAll(set);
		
		if(flag1)
			System.out.println("miao bu jian le");
		else
			System.out.println("miao hai zai");
```
#### Map
- Map中的数据是以键值对(key-value)的形式存储的
- key-value以Entry类型的对象实例存在
- 可以通过key值快速查找value
- 一个映射不能包含重复的健
- 每个键最多只能映射到一个值
#### HashMap
- 基于哈希表的Map接口的实现
- 允许使用null和null健
- key值不允许重复
- HashMap中的Entry对象是无序排列的