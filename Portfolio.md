# Portfolio

[Home](home.md) 

[About](About.md) 

[Portfoilio](Portfolio.md) 

[CV](CV.md) 

[Contacts](Contact.md) 

## Coding Minds Project Code

### Flutter Todo List Code 
This is code I made with a student for his flutter note taking app. 
This is the note list page, which uses firebase as a database to host notes to.

```java
import 'package:firebase_database/firebase_database.dart';
import 'package:flutter/material.dart';
import 'package:this_is_a_project/thisisafile.dart';
import 'package:this_is_a_project/wahooo.dart';
import 'database.dart';
import 'Widgets.dart';
import 'main.dart';
import 'package:page_transition/page_transition.dart';
class notelist extends StatefulWidget {
  const notelist ({Key? key, required this.title})
      : super(key: key);

  // This widget is the home page of your application. It is stateful, meaning
  // that it has a State object (defined below) that contains fields that affect
  // how it looks.

  // This class is the configuration for the state. It holds the values (in this
  // case the title) provided by the parent (in this case the App widget) and
  // used by the build method of the State. Fields in a Widget subclass are
  // always marked "final".

  final String title;

  @override
  State<lettheembarassmentcommence> createState() =>
      _lettheembarassmentcommenceState();
}

class notelistState extends State<notelist>{
  String url="";
  DatabaseHelper db= DatabaseHelper();
  List<taskpage> data = [];

  List<dynamic> thisisalist = [];
 //listening ofr firebase changes
  notelistState() {
    refreshNotes();
    FirebaseDatabase.instance.ref().child("tasks").onChildChanged.listen((event) {
      print("Data changed!");
      refreshNotes();
    });
    FirebaseDatabase.instance.ref().child("tasks").onChildRemoved.listen((event) {
      refreshNotes();
    });
    FirebaseDatabase.instance.ref().child("tasks").onChildAdded.listen((event) {
      refreshNotes();
    });
  }
  //refresh the taskpage array data
  void refreshNotes() {
  FirebaseDatabase.instance.ref().child('tasks').once().then((event) {
  List<taskpage> notetmplist = [];
  bool toggledelete = false;
  for (DataSnapshot i in event.snapshot.children){
  // title = event.snapshot.children.elementAt(i).value.toString();

  setState( () => notetmplist.add(taskpage(
  i.children.elementAt(2).value.toString(),
  i.children.elementAt(1).value.toString(),
  i.children.elementAt(0).value.toString()
  )));
  };
  data = notetmplist;
  });
}



  @override
  void initState() {
    DatabaseReference _db1 = FirebaseDatabase.instance.ref();
    var ref = _db1.child('tasks');
    ref.onValue.listen((event) {
      //i = 0;
      int x = event.snapshot.children.length;
      print(x);
      data.clear();
      int t = 0;
      for (DataSnapshot i in event.snapshot.children){
        // title = event.snapshot.children.elementAt(i).value.toString();

        setState(() => data.insert(t, (taskpage(
            i.children.elementAt(2).value.toString(),
          i.children.elementAt(1).value.toString(),
          i.children.elementAt(0).value.toString(),

        ))));
        // data[t] = TaskCardWidget(i.children.elementAt(1).value.toString(), i.children.elementAt(0).value.toString());
        t++;
      };
    });
    super.initState();
  }

  void list() async {
    setState(() => data = db.getValue());
    print(data);
  }

  void thisisaloop() {
    Navigator.push(context,
        MaterialPageRoute(builder: (context) => nextpage(title: "I give up")));
  }


  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(automaticallyImplyLeading: false,title: Row(
          children: <Widget>[
        IconButton(
        icon: Icon(Icons.arrow_back_ios),
        onPressed: () {
          Navigator.push(
              context,
              PageTransition(type: PageTransitionType.leftToRight, child: wahooo(thisisalist,"Editing Page", url,)));
        },
      ),
          Text(widget.title)
          ]),
        actions:[


      IconButton(
        icon: Icon(Icons.arrow_forward_ios),
        onPressed: () {
          Navigator.push(
              context,
              MaterialPageRoute(
                  builder: (context) => MyHomePage(title:"recording page")));

        },
      )]

      ),
      body: SingleChildScrollView(
        reverse: true,
        // Center is a layout widget. It takes a single child and positions it
        child: Padding(
          padding: EdgeInsets.all(10.0),
          child: Column(

            mainAxisAlignment: MainAxisAlignment.center,
            children: data,

          ),
        ),
      ),
    );
  }
}
```


### Unity Game Code 
This is code I made for a Unity Curriculum Project which showed students how to build a Tic Tac Toe Game from UI 
Here is the main TicTacToe Script
```cs
using System.Collections;
using System.Collections.Generic;
using UnityEngine;
using UnityEngine.UI;
using UnityEngine.EventSystems;

public class TicTacToe : MonoBehaviour
{
    public Transform buttonHolder;
    public Sprite X;
    public Sprite O;
    public Sprite normal;
    public int turn = 0; //x is 0, O is 1

    public void ButtonClick() 
    {
        string ClickedButtonName = EventSystem.current.currentSelectedGameObject.name;
        GameObject button = GameObject.Find(ClickedButtonName);
        if (turn == 0)
        {
            button.GetComponent<Image>().sprite = X;
            button.GetComponent<Button>().interactable = false;
            turn = 1;
        }
        else {
            button.GetComponent<Image>().sprite = O;
            button.GetComponent<Button>().interactable = false;
            turn = 0;
        }
    }


    public void Reset()
    {
        for (int i = 0; i < 9; i++)
        {
            buttonHolder.GetChild(i).gameObject.GetComponent<Button>().interactable = true;
            buttonHolder.GetChild(i).gameObject.GetComponent<Image>().sprite = normal;

        }
    }

}
```



### Pure Data Programming
This is an example of Pure Data Programming here I am creating acouple of simple effects for a sound. 
The effects created are an AR envolpe, Octave Switch, and Auto Panning.
![](https://cdn.discordapp.com/attachments/969018400695259199/1025539969839808605/unknown.png)






