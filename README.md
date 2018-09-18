##   APP Client - user Add 使用者註冊

POST：https://aplchat.apollogaming.net/user/add

Header：Content-Type     
Value：application/json

    {
      "username": "A123456",
      "nick":	"N123456",
      "password": "P123456"
    }
    
return

    {
        "success": true,
        "user": {
            "user_id": 26,
            "username": "A12345671",
            "password": "c5a9dcbefa6e0a11d7fc25645edb2e761050c663601855106129eeca3ee02e52",
            "password_hash": "RDKJER",
            "nick": "N123456",
            "email": "",
            "add_time": 1533524001,
            "last_login_time": 0,
            "login_times": 0,
            "status": 0,
            "room_id": 0
        }
    }
    
	or
	
	{
        "msg": "帳號重複",
        "success": false
    }
				
##   APP Client - user Login 使用者登入


POST：https://aplchat.apollogaming.net/user/login

Header：Content-Type     
Value：application/json

    {
      "username": "A123456",
      "password": "P123456"
    }
    
return

    {
        "code": 200,
        "expire": "2018-08-03T18:59:28+08:00",
        "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJleHAiOjE1MzMyOTM5NjgsImlkIjoiQTEyMzQ1NiIsIm9yaWdfaWF0IjoxNTMzMjkwMzY4fQ.7O-iTJTztOaG8hnGS8NCsWIU7FVPR63SdwwX1zCkG0s"
    }



##   APP Client - get message from stream 讀取頻道訊息

listen：https://aplchat.apollogaming.net/chat/stream  

Header：Authorization    
Value：Bearer + {{token}}


##   APP Client - Send Messaage  傳送訊息

POST：https://aplchat.apollogaming.net/chat/send

Header：Authorization    
Value：Bearer + {{token}}


    {
      "msg_room_id": 10,
      "msg_message": "msg_1112"
    }
    
return

    {
        "msg_add_time": 1536301483,
        "msg_id": 807,
        "msg_message": "msg_1112",
        "msg_room_id": 10,
        "send_username": "U123456"
    }


##   APP Client - Read History Messaage 讀取歷史訊息

POST：https://aplchat.apollogaming.net/chat/read

Header：Authorization    
Value：Bearer + {{token}}

    [
      {
        "msg_room_id" : 10,
        "msg_id":800
      },
      {
        "msg_room_id" : 11,
        "msg_id":580
      }
    ]
    
return

    [
        {
            "msg_id": 802,
            "send_username": "U123456",
            "msg_room_id": 10,
            "msg_add_time": 1536301324,
            "msg_message": "msg_1112"
        },
        {
            "msg_id": 805,
            "send_username": "U123456",
            "msg_room_id": 10,
            "msg_add_time": 1536301372,
            "msg_message": "msg_1112"
        },
        {
            "msg_id": 807,
            "send_username": "U123456",
            "msg_room_id": 10,
            "msg_add_time": 1536301483,
            "msg_message": "msg_1112"
        },
        {
            "msg_id": 590,
            "send_username": "WEB-001U",
            "msg_room_id": 11,
            "msg_add_time": 1534907233,
            "msg_message": "666666"
        },
        {
            "msg_id": 644,
            "send_username": "WEB-001U",
            "msg_room_id": 11,
            "msg_add_time": 1535006784,
            "msg_message": "666"
        }
    ]


##   APP Client - Add Room  ，創立 Room

POST：https://aplchat.apollogaming.net/chatroom/add

Header：Authorization    
Value：Bearer + {{token}}

    {
      "room_name": "Hello Room 111"
    }
    
return

     {
         "map_id": 34,
         "room_id": 19,
         "room_name": "Hello Room 111",
         "success": true
     }
     
     
     
##   APP Client - Join Room  ，邀請進群，單次多人

POST：https://aplchat.apollogaming.net/chatroom/join

Header：Authorization    
Value：Bearer + {{token}}

    {
      "map_room_id": 10,
      "map_username": [
        "D123456",
        "E123456"
      ]
    }
    
return

    {
        "membersNum": 2,
        "room_id": 10,
        "success": true
    }
    
    
##   APP Client - Kick Room  ，刪除成員

POST：https://aplchat.apollogaming.net/chatroom/kick

Header：Authorization    
Value：Bearer + {{token}}

    {
      "map_room_id": 10,
      "map_username": "B123456"
    }
    
return

    {
        "map_username": "B123456",
        "msg": "剔除成員",
        "success": true
    }
    

##   APP Client - List Members  ，成員清單

POST：https://aplchat.apollogaming.net/chatroom/listmembers

Header：Authorization    
Value：Bearer + {{token}}

    {
      "map_room_id": 10,
    }
    
return

    {
        "members": [
            "U123456",
            "AAAAAA",
            "Brook123",
            "Nadal999",
            "A123456"
        ],
        "room_id": 10,
        "success": true
    }
