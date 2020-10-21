# 泛型
- 在Java中增加泛型之前，泛型程序设计使用继承来实现的
- 坏处：
  - 需要强制转换
  - 可向集合中添加任意类型的对象，存在风险
  ### 泛型作为方法参数

  ```
  package pers.java.generic;

  public class TwoNumGeneric<T,X> {
    private T num1;
    private X num2;
    public void genNum(T num1,X num2) {
      this.num1 = num1;
      this.num2 = num2;
    }
    public T getNum1() {
      return num1;
    }
    public void setNum1(T num1) {
      this.num1 = num1;
    }
    public X getNum2() {
      return num2;
    }
    public void setNum2(X num2) {
      this.num2 = num2;
    }
    public static void main(String[] args) {
      TwoNumGeneric<Integer,Float> numObj = new TwoNumGeneric<>();
      numObj.genNum(21, 1.2f);
      System.out.println(numObj.getNum1()+" "+numObj.getNum2());
    }
  }
  ```
 ### 自定义泛型方法

 ```
public <T> void printValue(T t) {
		System.out.println(t);
}
public static void main(String[] args) {
		GenericMethod gm = new GenericMethod();
		gm.printValue("str");
}
 ```
