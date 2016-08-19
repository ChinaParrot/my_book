# 表单详解

表单是一个包含表单元素的区域。
表单元素是允许用户在表单中输入内容,比如：文本域(textarea)、下拉列表、单选框(radio-buttons)、复选框(checkboxes)等等。



实例：
```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Form</title>
</head>
<body>
    <div style="text-align: center;">
        <h1>用户注册</h1>
        <hr>
        <form action="sucess.html">
            <table   border="0" cellspacing="0" cellpadding="0" align="center">
                <tr>
                    <td>用户名：</td>
                    <td><input type="text" name="uername" /></td>
                </tr>
                <tr>
                    <td>密码：</td>
                    <td><input type="password" name="password"/></td>
                </tr>
                <tr>
                    <td>确认密码：</td>
                    <td><input type="password" name="confirmpass"/></td>
                </tr>
                  <tr>
                    <td>电子邮箱：</td>
                    <td><input type="text" name="email" /></td>
                </tr>

                  <tr>
                    <td>性别：</td>
                    <td>
                        <input type="radio" name="gender" value="1" checked/>男
                        <input type="radio" name="gender" value="0"/>女
                    </td>
                </tr>

                <tr>
                    <td>学历：</td>
                    <td>
                        <select name="education" >
                            <option value="-1" selected>--请选择--</option>
                            <option value="0">小学</option>
                            <option value="1">初中</option>
                            <option value="2">高中</option>
                            <option value="3">大专</option>
                            <option value="4">本科</option>
                        </select>
                    </td>
                </tr>

                <tr>
                    <td>爱好：</td>
                    <td>
                        <input type="checkbox" name="favorite" value="read" /> 读书
                        <input type="checkbox" name="favorite" value="movie" /> 电影
                        <input type="checkbox" name="favorite" value="music" /> 音乐
                        <input type="checkbox" name="favorite" value="internet"/> 上网
                        <input type="checkbox" name="favorite" value="other"/> 其他                    </td>
                </tr>
                <tr>
                    <td>服务协议：</td>
                    <td>
                        <textarea rows="10" cols="15">
                            霸王条款，霸王条款霸王条款霸王条款霸王条款霸王条款霸王条款霸王条款霸王条款霸王条款霸王条款
                            霸王条款霸王条款霸王条款霸王条款霸王条款霸王条款霸王条款霸王条款霸王条款霸王条款
                            霸王条款霸王条款霸王条款霸王条款霸王条款霸王条款霸王条款霸王条款霸王条款霸王条款霸王条款霸王条款霸王条款霸王条款

                        </textarea>
                    </td>
                </tr>

                <tr>
                    <td>是否接受协议：</td>
                    <td>
                        <input type="checkbox" name="isaccept" checked/>
                    </td>
                </tr>
                <tr>
                    <td>上传头像：<td>
                    <td><input type="file" name="picture"></td>
                </tr>
                <tr>
                    <td colspan="2" align="center">
                        <input type="submit" value="注册" />
                        <input type="reset" value="取消">
                    </td>
                </tr>

            </table>
        </form>
    </div>
</body>
</html>
```

