import 'package:flutter/material.dart';
import 'package:login_app/ForgotPassword.dart';
import 'package:login_app/HomePage.dart';
import 'package:login_app/Register.dart';

class Login extends StatefulWidget {
  @override
  _LoginState createState() => _LoginState();
}

class _LoginState extends State<Login> {
  String userName;
  String password;
  final _formKey = GlobalKey<FormState>();
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      resizeToAvoidBottomPadding: false,
      body: Form(
        key: _formKey,
        child: Column(
          mainAxisAlignment: MainAxisAlignment.center,
          children: [
            Padding(
              padding: const EdgeInsets.only(left: 20,right: 20),
              child: TextFormField(
                decoration: InputDecoration(
                  focusedBorder: OutlineInputBorder(
                    borderSide: BorderSide(color: Colors.purple)
                  ),
                  labelText: "Kullanıcı Adı",
                  labelStyle: TextStyle(color: Colors.purple),
                  border: OutlineInputBorder(),
                ),
                validator: (value){
                  if(value.isEmpty){
                    return "Kullanıcı Adı Giriniz";
                  }else{
                    return null;
                  }
                },
                onSaved: (value) {
                    userName=value;
                },
              ),
            ),
            SizedBox(height: 20,),
            Padding(
              padding: const EdgeInsets.only(left: 20,right: 20),
              child: TextFormField(
                decoration: InputDecoration(
                  focusedBorder: OutlineInputBorder(
                      borderSide: BorderSide(color: Colors.purple),
                  ),
                  labelText: "Parola",
                  labelStyle: TextStyle(color: Colors.purple),
                  border: OutlineInputBorder(),

                ),
                validator: (value){
                  if(value.isEmpty){
                    return "Parolanızı Giriniz";
                  }else{
                    return null;
                  }
                },
                onSaved: (value) {
                  password=value;
                },
              ),
            ),
            Row(
              mainAxisAlignment: MainAxisAlignment.spaceBetween,
              children: [
                MaterialButton(
                  child: Text("Üye Ol"),
                  onPressed: (){
                    Navigator.push(context,MaterialPageRoute(builder: (context) => Register()));
                  },
                ),
                MaterialButton(
                  child: Text("Şifremi Unuttum"),
                  onPressed: (){
                    Navigator.push(context,MaterialPageRoute(builder: (context) => Forgot()));
                  },
                )
              ],
            ),
            _loginButton(),
          ],
        ),
      ),
    );
  }
  Widget _loginButton() =>
      RaisedButton(child: Text("Giriş Yap"), onPressed: (){
        if(_formKey.currentState.validate()){
          _formKey.currentState.save();
          if(userName == "demo" && password == "demo"){
            showDialog(context: context,
            builder: (BuildContext context){
              return AlertDialog(
                title: Text("Giriş"),
                content: Text("Giriş Başarılı Yönlendiriliyorsunuz"),
                actions: [
                  MaterialButton(
                    child: Text("Devam"),
                    onPressed: () => Navigator.push(context,MaterialPageRoute(builder: (context) => Home()))
                  )
                ],
              );
            }
            );
          }else {
            showDialog(
                barrierDismissible: false,
                context: context,
                builder: (BuildContext context){
                  return AlertDialog(
                    title: Text("Hata"),
                    content: Text("Giriş Bilgileri Hatalı"),
                    actions: [
                      MaterialButton(
                        child: Text("Geri Dön"),
                        onPressed: () => Navigator.pop(context),
                      )
                    ],
                  );
                }
            );
          }
        }
      },);
}
