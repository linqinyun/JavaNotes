# Java输入输出流
## File类的使用
    getName()：返回文件名称。
    getParent()：返回文件父目录路径。
    getPath()：返回文件的潜在相对路径。
    getParentFile()：返回文件所在文件夹的路径。
```
File file = new File("D:\\notes\\io\\Monday.docx");
		//是否存在文件
		if(!file.exists()) {
			try {
				//创建文件
				file.createNewFile();
			} catch (IOException e) {
				// TODO Auto-generated catch block
				e.printStackTrace();
			}
			System.out.println("文件创建成功");
		}else {
			//返回文件名称
			//返回父目录
			System.out.println("文件已存在");
		}
		//是否文件
		if(file.isFile()) {//文件
			//返回文件名称
			//返回父目录
			System.out.println("文件名称："+file.getName());
			System.out.println("文件的上一级目录："+file.getParentFile().getName());
			System.out.println("这是文件");
		}else if(file.isDirectory()) {//目录
			System.out.println("这是目录");
		}else {
			//不是目录和文件
			System.out.println("既不是文件也不是目录");
		}

		if(file.canWrite()&&file.canRead()) {
			System.out.println("读写性:这个文件可读可写");	
		}else if(file.canWrite()||file.canRead()){
			if(file.canWrite()) {
				System.out.println("读写性:这个文件可写");	
			}else {
				System.out.println("读写性:这个文件不可写");
			}
			if(file.canRead()) {
				System.out.println("读写性:这个文件可读");	
			}else {
				System.out.println("读写性:这个文件不可读");
			}
		}else {
			System.out.println("读写性:这个文件不可读/写");
		}
```
### 绝对路径与相对路径
```
//判断绝对路径还是相对路径
    file.isAbsolute();`
```
## 字节流
- 字节输入流InputStream
    - 从文件系统中某个文件中获得输入字节
    - 用于读取诸如图像数据之类的原始字节流
```
try {
			FileInputStream fls = new FileInputStream("javaSt.txt");
//			int n = fls.read();
			int n = 0;
//			while(n!=-1) {
//				System.out.print((char)n);
//				n = fls.read();
//			}
			while((n=fls.read())!=-1) {
				System.out.print((char)n);
			}
			fls.close();
		} catch (FileNotFoundException e) {
			// TODO Auto-generated catch block
			e.printStackTrace();
		} catch (IOException e) {
			e.printStackTrace();
		}
```
```
		try {
			FileInputStream fls = new FileInputStream("javaSt.txt");
			byte[] b = new byte[100];
			fls.read(b);
			System.out.println(new String(b));
			fls.close();
		} catch (FileNotFoundException e) {
			// TODO Auto-generated catch block
			e.printStackTrace();
		} catch (IOException e) {
			e.printStackTrace();
		}
```
```
		File fl = new File("javaSt.txt");
		try {
			FileInputStream fls = new FileInputStream(fl);
			int count = 0;
			int n = 0;
			System.out.print("文本内容:");
			while((n=fls.read())!=-1) {
				System.out.print((char)n);
				count++;
			}
			System.out.println();
			System.out.println("统计结果："+fl.getName()+" 字符: "+count);
		} catch (FileNotFoundException e) {
			// TODO Auto-generated catch block
			e.printStackTrace();
		} catch (IOException e) {
			// TODO Auto-generated catch block
			e.printStackTrace();
		}
```
- 字节输出流OutoutStream
	-	数据写入
	```
	//输出流-FileOutputStream，数据写入
		FileOutputStream fos;
		FileInputStream fis;
		try {
			//为true表示追加，默认false
			fos = new FileOutputStream("javaSt.txt",true);
			fis =new FileInputStream("javaSt.txt");
			fos.write(50);
			fos.write('a');
			System.out.println(fis.read());
			System.out.println((char)fis.read());
			fos.close();
			fis.close();
		} catch (FileNotFoundException e) {
			// TODO Auto-generated catch block
			e.printStackTrace();
		} catch (IOException e) {
			// TODO Auto-generated catch block
			e.printStackTrace();
		} 
	```
	- 数据拷贝
	```
	// 文件拷贝
		try {
			FileInputStream fis = new FileInputStream("happy.jpg");
			FileOutputStream fos = new FileOutputStream("happycopy.jpg");
			int n = 0;
			byte[] b=new byte[1024];
			while((n=fis.read(b))!=-1) {
				fos.write(b,0,n);
			}
			fis.close();
			fos.close();
		} catch (FileNotFoundException e) {
			// TODO Auto-generated catch block
			e.printStackTrace();
		} catch (IOException e) {
			// TODO Auto-generated catch block
			e.printStackTrace();
		}
	```
- 缓冲输入流BufferedInputStream
- 缓冲输出流BufferedOutputStream
```
try {
			FileOutputStream fos = new FileOutputStream("javaSt.txt");
			BufferedOutputStream bos = new BufferedOutputStream(fos);
			FileInputStream fis = new FileInputStream("javaSt.txt");
			BufferedInputStream bis = new BufferedInputStream(fis);
			long startTime = System.currentTimeMillis();
			bos.write(50);
			bos.write('a');
			bos.flush();
			System.out.println(bis.read());
			System.out.println((char)bis.read());
			long endTime = System.currentTimeMillis();
			System.out.println(endTime-startTime);
			bos.close();
			fos.close();
			fis.close();
			bis.close();
		} catch (FileNotFoundException e) {
			// TODO Auto-generated catch block
			e.printStackTrace();
		} catch (IOException e) {
			// TODO Auto-generated catch block
			e.printStackTrace();
		}
```
## 字符流
- 字符输入流Reader
- 字符输出流Writer
- 字节字符转换流
	- InputStreamReader
	- OutputStreamWriter
	```
	String filePath = "D:\\notes\\io\\test.txt";
		String filePath1 = "D:\\notes\\io\\test1.txt";
		try {
			FileInputStream fis = new FileInputStream(filePath);
			InputStreamReader isr = new InputStreamReader(fis);
			FileOutputStream fos = new FileOutputStream(filePath1);
			OutputStreamWriter osw = new OutputStreamWriter(fos);
			int n = 0;
			char[] cbuf = new char[10];
//			while((n=isr.read())!=-1) {
//				System.out.print((char)n);
//			}
//			while((n=isr.read(cbuf))!=-1) {
//				String s = new String(cbuf,0,n);
//				System.out.print(s);
//			}
			while((n=isr.read(cbuf))!=-1) {
				String s = new String(cbuf,0,n);
//				osw.write(s);
				osw.write(cbuf,0,n);
				osw.flush();
			}
			fis.close();
			fos.close();
			isr.close();
			osw.close();
		} catch (FileNotFoundException e) {
			// TODO Auto-generated catch block
			e.printStackTrace();
		} catch (IOException e) {
			// TODO Auto-generated catch block
			e.printStackTrace();
		}
	```
	- 其他字符流
## 对象的序列化与反序列化
序列化步骤：  
1. 创建一个类，继承Serializable接口
（只有当类继承了Serializable接口才能序列化与反序列化）
2. 创建该类的对象
3. 因为ObjectOutputStream()参数为字节流所以要先创建一个字节流的对象
FileOutputStream fos=new FileOutputStream("imooc.txt");
4. 创建序列化对象ObjectOutputStream oos=new ObjectOutputStream(fos)
5. 将一开始创建的对象写入文件  
oos.writeObject(good1);  
oos.flush()  

从文件读取对象信息(反序列化)  
1. FileInputStream fis=new FileInputStream("imooc.txt");
2. ObjectInputStream ois=new ObjectInputStream(fis)
3. 调用ois.readObject()方法，因为该方法返回值为object类型所以应该强制转换
4. Goods goods=(Good)ois.readObject();
5. 直接输出重写过toString方法的类

同样也可以序列化其他类型  

例  
写入：  
oss.writeBoolean(true);  
读取：  
System.out.println(ois.readBoolean());  

注：反序列化时应当按照序列化的顺序读取，否则将会报EOFException异常
因为读取不会分辨特定的类型，第一次写入的类型时GOOD 第二次是boolean。读取时不论用哪种方式都只会先读取GOOD类型，读取的类型和写入的类型不一样就会报错

ObjectInputStream 对象输入流类  
ObjectOutputStream 对象输出流类  
