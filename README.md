# 2024-05-22


import 'package:flutter/material.dart';
import 'package:url_launcher/url_launcher.dart';

void main() {
  runApp(UserApp());
}

class UserApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: '사용자 앱',
      theme: ThemeData(
        primarySwatch: Colors.blue,
      ),
      home: UserHomePage(),
    );
  }
}

class UserHomePage extends StatelessWidget {
  final String adminAppUrl = 'adminapp://'; // 관리자 앱의 URL 스킴

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('사용자 앱'),
      ),
      body: Center(
        child: Column(
          mainAxisAlignment: MainAxisAlignment.center,
          children: <Widget>[
            ElevatedButton(
              onPressed: () {
                sendRequest('외출');
              },
              child: Text('외출 신청'),
            ),
            ElevatedButton(
              onPressed: () {
                sendRequest('외박');
              },
              child: Text('외박 신청'),
            ),
          ],
        ),
      ),
    );
  }

  void sendRequest(String type) async {
    String url = '$adminAppUrl?type=$type';
    if (await canLaunch(url)) {
      await launch(url);
    } else {
      throw '관리자 앱을 열 수 없습니다.';
    }
  }
}
