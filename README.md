# 使用者
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


# 聊天訊息
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
            "msg_id": 644,
            "send_username": "WEB-001U",
            "msg_room_id": 11,
            "msg_add_time": 1535006784,
            "msg_message": "666"
        }
    ]

# 聊天室
##   APP Client - Add Room  ，創立 Room

POST：https://aplchat.apollogaming.net/chat_room

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
     
##   APP Client - List Room  ， Room 清單

GET：https://aplchat.apollogaming.net/chat_room

Header：Authorization    
Value：Bearer + {{token}}

return

    [
        {
            "room_id": 5,
            "room_name": "Hi Room 5"
        },
        {
            "room_id": 21,
            "room_name": "Hello Room 222"
        }
    ]
     
     
# 聊天室成員
##   APP Client - Join Room  ，邀請進群，單次多人

POST：https://aplchat.apollogaming.net/room_member

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

DELETE：https://aplchat.apollogaming.net/room_member

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

POST：https://aplchat.apollogaming.net/room_member/list

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
    
    
# 好友名單管理
##   APP Client - Check User  ，確認用戶存在

POST：https://aplchat.apollogaming.net/friend/check

Header：Authorization    
Value：Bearer + {{token}}

    {
      "username": "B123456"
    }
    
return

    {
        "nick": "N123456",
        "success": true,
        "username": "B123456"
    }
    
##   APP Client - Add Friend  ，加入好友

POST：https://aplchat.apollogaming.net/friend

Header：Authorization    
Value：Bearer + {{token}}

    {
      "friend_mapping_name": "B123456"
    }
    
return

    {
        "nick": "N123456",
        "success": true,
        "username": "B123456"
    }
    
##   APP Client - DEL Friend  ，刪除好友

DELETE：https://aplchat.apollogaming.net/friend

Header：Authorization    
Value：Bearer + {{token}}

    {
      "friend_mapping_name": "C123456"
    }
    
return

    {
        "msg": "已刪除好友",
        "success": true,
        "username": "C123456"
    }
    
##   APP Client -  Friend List ，好友清單

GET：https://aplchat.apollogaming.net/friend

Header：Authorization    
Value：Bearer + {{token}}
    
return

    [
        {
            "username": "B123456",
            "nick": "N123456"
        },
        {
            "username": "A123456",
            "nick": "N123456"
        }
    ]
	
	
