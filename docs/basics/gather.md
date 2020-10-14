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