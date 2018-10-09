# 使用者
##   APP Client - user Add 使用者註冊

POST：https://aplchat.apollogaming.net/user/add

Header：Content-Type     
Value：application/json

    {
      "username": "F123456",
      "nick":	"N123456",
      "password": "P123456"
    }
    
return

    {
        "success": true,
        "user_id": 116,
        "username": "F123456"
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
        "msg_user_id": 37
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
            "msg_user_id": 37,
            "msg_room_id": 10,
            "msg_add_time": 1536301324,
            "msg_message": "msg_1112"
        },
        {
            "msg_id": 644,
            "msg_user_id": 37,
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

空群(多人),無邀請成員：

    {
      "room_name": "Hello Room 111"
    }

1V1,創room並邀請：

    {
      "msg_user_id": 37
    }
    
return

     {
         "room_id": 19,
         "room_name": "Hello Room 111",
         "success": true
     }
     
##   APP Client - Edit Room  ，修改 Room Name

PUT：https://aplchat.apollogaming.net/chat_room

Header：Authorization    
Value：Bearer + {{token}}

    {
      "room_id": 10,
      "room_name": "Room 2222"
    }
    
return

    {
        "room_id": 10,
        "room_name": "Room 2222",
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
     
##   APP Client - List Room  ， Room + Last MSG ID 清單 

GET：https://aplchat.apollogaming.net/chat_room/msg

Header：Authorization    
Value：Bearer + {{token}}

return

    [
        {
            "room_id": 5,
            "room_name": "room-5",
            "msg_id": 2441
        },
        {
            "room_id": 10,
            "room_name": "Room 2222",
            "msg_id": 2462
        }
    ]
     
# 聊天室成員
##   APP Client - Join Room  ，邀請進群，單次多人

POST：https://aplchat.apollogaming.net/room_member

Header：Authorization    
Value：Bearer + {{token}}

    {
      "map_room_id": 10,
      "map_user_id": [
        113,
        114
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
      "msg_user_id" 37
    }
    
return

    {
        "msg_user_id" 37,
        "msg": "剔除成員",
        "success": true
    }
    

##   APP Client - List Members  ，成員清單

POST：https://aplchat.apollogaming.net/room_member/list

Header：Authorization    
Value：Bearer + {{token}}

    {
      "map_room_id": 10
    }
    
return

    {
        "members": [
            {
                "user_id": 37,
                "nick": "N123456"
            },
            {
                "user_id": 1,
                "nick": "N123456"
            },
            {
                "user_id": 113,
                "nick": "N123456"
            }
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
        "user_id": 113
    }
    
##   APP Client - Add Friend  ，加入好友

POST：https://aplchat.apollogaming.net/friend

Header：Authorization    
Value：Bearer + {{token}}

    {
      "fd_map_user_id": 37
    }
    
return

    {
        "nick": "N123456",
        "success": true,
        "fd_map_user_id": 113
    }
    
##   APP Client - DEL Friend  ，刪除好友

DELETE：https://aplchat.apollogaming.net/friend

Header：Authorization    
Value：Bearer + {{token}}

    {
      "fd_map_user_id": "B123456"
    }
    
return

    {
        "msg": "已刪除好友",
        "success": true,
        "fd_map_user_id": 113
    }
    
##   APP Client -  Friend List ，好友清單

GET：https://aplchat.apollogaming.net/friend

Header：Authorization    
Value：Bearer + {{token}}
    
return

    [
        {
            "user_id": 113,
            "nick": "N123456"
        },
        {
            "user_id": 1,
            "nick": "N123456"
        }
    ]
