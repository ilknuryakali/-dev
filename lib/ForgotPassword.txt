import 'package:flutter/material.dart';

class Forgot extends StatefulWidget {
  @override
  _ForgotState createState() => _ForgotState();
}

class _ForgotState extends State<Forgot> {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
       body: Form(
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

               ),
             ),
             _forgotButton(),
           ],
         ),
       ),
    );
  }

  Widget _forgotButton() =>
      RaisedButton(child: Text("Şifremi Sıfırla"), onPressed: (){
        showDialog(
            barrierDismissible: false,
            context: context,
            builder: (BuildContext context){
              return AlertDialog(
                title: Text("Bilgilendirme"),
                content: Text("Şifre Sıfırlama İşlemi İçin Gerekli Bilgiler Yönlendirildi"),
                actions: [
                  MaterialButton(
                    child: Text("Geri Dön"),
                    onPressed: () => Navigator.pop(context),
                  )
                ],
              );
            }
        );
      },);
  
}
