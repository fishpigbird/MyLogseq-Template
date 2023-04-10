-
	- [[dailynote]]和[[双链]]需要层级缩进，后期整理。
	  collapsed:: true
		- 当我们把双链放到顶级bullet时，神奇的事情就会发生。不仅双链会形成，反链还会看到内容。
			- 当一个node的子级下有其他node时，只有当这个node整理到其位置时。
				- 双链结构和回显才会生成。
-
	- #2023-04-11
		- **02:18**  成功将昨天 [[dailynote]] Java添加日期代码转换为了 [[Sublime Text 3/Plugin]]。
		  id:: 6434579c-4f76-4e04-8c1e-728b3309dc0f
			- 尝试过程
				- 首先尝试写 [[logseq/plugin]]，并借助 [[AI]]来学习编写，因为相关教程比较少，不过还是主要因为涉及到JS代码，但其与Java差距过大，无法迅速理解，遂放弃此方法。
				- 其次则准备GPT3.5将Java代码转换为Sublime支持的Python3.3代码，作为其插件使用。但GPT3.5的代码理解能力着实有点菜了，具体我就不展示了。
			- 最终用GPT4进行代码转换，几乎一次成功。请欣赏：
				- Code
				  background-color:: red
				  collapsed:: true
					- ```java
					  import sublime
					  import sublime_plugin
					  import re
					  import os
					  
					  class LogseqJournalsDateCommand(sublime_plugin.TextCommand):
					      def run(self, edit):
					          file_path = self.view.file_name()
					          print(file_path)
					          process_file(file_path)
					  
					  #以下代码通过GPT4生成，它完美的将java逻辑转换为了Python代码。仅仅有一处错误。
					  #相比较GPT3.5而言，提升巨大。
					  # 一个检查字符串是否匹配模式 #YYYY-MM-DD 的方法
					  def is_date(s):
					      p = re.compile(r'#\d{4}-\d{2}-\d{2}')
					      m = p.search(s)
					      return m is not None
					  
					  # 一个处理单个文件的方法
					  def process_file(file_path):
					      try:
					          # 读取文件
					          with open(file_path, 'r', encoding='utf-8') as file:
					              lines = file.readlines()
					  
					          # 获取文件名
					          name, _ = os.path.splitext(os.path.basename(file_path))
					  
					          # 创建一个列表来存储修改后的内容
					          modified_lines = []
					          i = 0
					          while i < len(lines):
					              line = lines[i].rstrip()
					              # 如果行只包含“-”，跳过它并读取下一行
					              if line == '-':
					                  modified_lines.append(line)
					                  i += 1
					                  while i < len(lines) and lines[i].strip() == '-':
					                      modified_lines.append(lines[i].rstrip())
					                      i += 1
					                  continue
					  
					              if line.startswith('-'):
					                  if is_date(line):
					                      modified_lines.append(line)
					                      i += 1
					                      while i < len(lines) and not lines[i].startswith('-'):
					                          modified_lines.append(lines[i].rstrip())
					                          i += 1
					                      ##GPT4仅仅忘记了这行
					                      continue
					                  else:
					                      date = name.replace('_', '-')
					                      modified_lines.append('- #' + date)
					                      modified_lines.append('\t' + line)
					              else:
					                  modified_lines.append('\t' + line)
					  
					              i += 1
					          # 将修改后的内容写回文件
					          with open(file_path, 'w', encoding='utf-8') as file:
					              file.write('\n'.join(modified_lines))
					  
					      except IOError as e:
					          print(e)
					  
					  ```
				- Sublime 插件使用教程
				  collapsed:: true
					- {{embed ((64341f75-92e6-48e0-b929-193dbfcf1743))}}
					-
				- ((64345711-ca91-4fba-a27a-d8b0e4226c8d))
			- 那么具体使用过程点击当日Journals，右上角三点，用默认文本打开，调用插件即可。
	- #2023-04-10
	  id:: 6434561b-89a2-4302-ae6f-2ae63801a033
		- 不会写插件，先写个 [[Sublime Text 3]]为 [[dailynote]]里的项目添加日期父级节点的吧。
		- 今天用[[java]]写了个给[[Logseq]] [[dailynote]] 内顶级block的小脚本，这样在后期整理的时候会非常方便，而且还不会丢失时间戳，代码目前没有优化，并且没有明显bug。 #logseq/plugin
		  id:: 6434561b-1eb9-41a8-9b6c-bc2e44ec08ae
			- 展示
			  collapsed:: true
				- ![image.png](../assets/image_1681067694146_0.png)
			- Code
			  background-color:: red
			  collapsed:: true
				- ```java
				  package org.example;
				  
				  import java.io.*;
				  import java.util.Scanner;
				  import java.util.regex.*;
				  
				  public class FileProcessor {
				  
				      // A method to check if a string matches the pattern #YYYY-MM-DD
				      public static boolean isDate(String s) {
				          Pattern p = Pattern.compile("#\\d{4}-\\d{2}-\\d{2}");
				          Matcher m = p.matcher(s);
				          return m.find();
				      }
				  
				      // A method to process a single file
				      public static void processFile(String fileName,String name) {
				          try {
				              // Create a buffered reader to read the file
				              BufferedReader br = new BufferedReader(new FileReader(fileName));
				  
				              // Create a string builder to store the modified content
				              StringBuilder sb = new StringBuilder();
				  
				              // Create a string variable to store the current date
				              String date = fileName;
				  
				              // Read each line of the file
				              String line = br.readLine();
				              while (line != null) {
				                  // If the line is only "-", skip it and read the next line
				                  if (line.equals("-")) {
				                      sb.append(line).append("\n");
				                      line = br.readLine();
				                      if (line != null) {
				                          int i = 0;
				                          while (i == 0) {
				                              if (line.trim().equals("-")) {
				                                  sb.append(line).append("\n");
				                                  line = br.readLine();
				                                  if (line == null ){
				                                      break;
				                                  }
				                              } else i = 1;
				                          }
				                          continue;
				                      }else {
				                          break;
				                      }
				  
				  
				                  }
				                  // If the line starts with "-", check the text after it
				                  if (line.startsWith("-")) {
				                      // Get the text after "-"
				                      // text = line.substring(1).trim();
				                      // If the text is a date, update the date variable and append the line to the string builder
				                      if (isDate(line)) {
				  
				                          sb.append(line).append("\n");
				  
				                          line = br.readLine();
				  
				                          if (line != null) {
				                              int i = 0;
				                              while (i == 0) {
				  
				                                  if (!line.startsWith("-")) {
				                                      sb.append(line).append("\n");
				                                      line = br.readLine();
				                                      if (line == null ){
				                                          break;
				                                      }
				                                  } else i = 1;
				                              }
				                              continue;
				                          }else {
				                              break;
				                          }
				  
				                      } else {
				                          // If the text is not a date, insert a date line before it and add a tab before the text
				                          date = name.replace("_", "-");;
				                          sb.append("- #").append(date).append("\n");
				                          sb.append("\t").append(line).append("\n");
				                      }
				                  } else {
				                      // If the line does not start with "-", add a tab before it and append it to the string builder
				                      // 和匹配到。
				                      sb.append("\t").append(line).append("\n");
				                  }
				  
				                  // Read the next line
				                  line = br.readLine();
				              }
				  
				              // Close the buffered reader
				              br.close();
				  
				              // Create a buffered writer to write the modified content to the file
				              BufferedWriter bw = new BufferedWriter(new FileWriter(fileName));
				  
				              // Write the string builder content to the file
				              bw.write(sb.toString());
				  
				              // Close the buffered writer
				              bw.close();
				  
				          } catch (IOException e) {
				              // Handle any IO exception
				              e.printStackTrace();
				          }
				      }
				  
				      public static void main(String[] args) {
				          // Get the start date and end date from user input
				  
				  
				  
				          Scanner sc = new Scanner(System.in);
				          String startDate;
				          String endDate;
				  
				          long start;
				          long end;
				  
				          int i = 1;
				          if (i == 0 ) {
				  
				              if (!sc.nextLine().equals("y")) {
				                  System.out.println("请输入开始日期（格式为YYYY_MM_DD）：");
				                  startDate = sc.nextLine();
				                  System.out.println("请输入结束日期（格式为YYYY_MM_DD）：");
				                  endDate = sc.nextLine();
				  
				              } else {
				                  startDate = "0";
				                  endDate = "99999999";
				  
				              }
				          }else {
				              startDate = "0";
				              endDate = "99999999";
				  
				          }
				  
				          sc.close();
				  
				          // Convert the dates to long values for comparison
				           start = Long.parseLong(startDate.replace("_", ""));
				           end = Long.parseLong(endDate.replace("_", ""));
				  
				          // Create a file object for the folder that contains the files
				          File folder = new File("D:\\Logseq\\journals");
				  
				          // Get an array of files in the folder
				          File[] files = folder.listFiles();
				  
				          // Loop through each file in the folder
				          for (File file : files) {
				              // Get the file name without extension
				              String fileName = file.getName().split("\\.")[0];
				  
				              // Convert the file name to a long value for comparison
				              long fileDate = Long.parseLong(fileName.replace("_", ""));
				  
				              // If the file name is within the start and end dates, process the file
				              if (fileDate >= start && fileDate <= end) {
				                  processFile(file.getPath(),fileName);
				              }
				          }
				      }
				  }
				  
				  ```
			- ((64345711-ca91-4fba-a27a-d8b0e4226c8d))
	- #2023-04-09
		- 写一个自动在 [[dailynote]]的顶级block前，添加当前日期插件。
		  id:: 6432550b-87e2-44ac-a2f9-c7ae704077ac
		  collapsed:: true
			- 请用java实现以下功能：
			  collapsed:: true
				- 请用java实现以下功能：
				- 背景信息
				  collapsed:: true
					- 变量 `filepath`用来传入windows系统的绝对目录。
					- 目录文件夹内的文件格式都是 `YYYY_MM_DD.txt`，例如 `2023_03_02.txt`。
					- 用户若输入 `all`，则读取文件夹内所有文件。用户若输入 `date`，则提醒用户输入开始日期和结束日期，然后依次通过字符流读取对应时间范围内的文件。
				- 字符处理过程
				  collapsed:: true
					- 若整行只有"-"字符，则不处理。
					- 若以"-"开头，且整行内的文本是有符合 `#\d\d\d\d-\d\d-\d\d`正则格式的，则一直读取下一行，每一行的内容都不做处理，直到碰到开头是“-”时，再重新进行判断。
					- 若"-" 后面的字符不符合 `#\d\d\d\d-\d\d-\d\d`正则格式的，则在此行行首，添加一个"制表符"，且在此行前插入 `- #YYYY-MM-DD\n`。且一直读取下一行，为每一行行首都添加"制表符"，直到碰到开头是“-”的，再重新进行判断。
				- new bing生成的代码可以用，但是不优雅。
				  collapsed:: true
					-
					-
					- 若开头是“制表符”的，一律在“制表符”前再添加一个“制表符”
					- 若开头是"-"的则分两种情况处理。
			- 判断是否已经为日期格式
			  collapsed:: true
				-
			- 1.读取文件流至String
			  2. 用正则 `- \w|- \[` 匹配 所有顶级层
			  3. 为匹配项前，添加一个 `制表符`
			  4. 用正则 `^	- \w|^	- \[` 匹配所有顶级层
			  5. 为匹配向前，添加 `- #filename.replace(_,-) \n`
			-
			- 用refs，
			- refs后用swap插件交换引用和本体。
-