-
	- [[Excel/VBA/Regex]]
		- 如何打开 [[Excel/VBA]]
			- [Excel VBA在哪 Excel VBA编辑器怎么打开-百度经验 (baidu.com)](https://jingyan.baidu.com/article/3f16e0031075a02590c1034e.html)
			- 文件格式另存为：xlsm
		- Regex
		  collapsed:: true
			- [Excel Regex to replace strings using regular expressions (ablebits.com)](https://www.ablebits.com/office-addins-blog/excel-regex-replace/)
			- ```vb
			  Public Function RegExpReplace(text As String, pattern As String, text_replace As String, Optional instance_num As Integer = 0, Optional match_case As Boolean = True) As String
			      Dim text_result, text_find As String
			      Dim matches_index, pos_start As Integer
			      On Error GoTo ErrHandl
			      
			      text_result = text
			      
			      Set regex = CreateObject("VBScript.RegExp")
			      
			      regex.pattrn = pattern
			      regex.Global = True
			      regex.MultiLine = True
			      
			      If True = match_case Then
			          regex.ignorecase = False
			      Else
			          regex.ignorecase = True
			      End If
			      
			      Set matches = regex.Execute(text)
			          
			      If 0 < matches.Count Then
			          If (0 = instance_num) Then
			              text_result = regex.Replace(text, text_replace)
			          Else
			              If instance_num <= matches.Count Then
			                  pos_start = 1
			                  For matches_index = 0 To instance_num - 2
			                      pos_start = InStr(pos_start, text, matches.Item(matches_index), vbBinaryCompare) + Len(matches.Item(matches_index))
			                  Next matches_index
			                  
			                  text_find = matches.Item(instance_num - 1)
			                  text_result = Left(text, pos_start - 1) & Replace(text, text_find, text_replace, pos_start, 1, vbBinaryCompare)
			              End If
			          End If
			      End If
			      
			      RegExpReplace = text_result
			      Exit Function
			  
			  ErrHandl:
			      RegExpReplace = CVErr(xlErrValue)
			  End Function
			  
			  ```