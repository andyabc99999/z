# 使用者
				
##   APP Client - user Login 使用者登入

POST：https://aplchat.apollogaming.net/user/login

Header：Content-Type     
Value：application/json

    {
      "username":   "chatroom1",
      "password":   "aa123456"
      "tpl":        "dio999"
    }
    
return

    {
        "code": 200,
        "expire": "2018-08-03T18:59:28+08:00",
        "id": 515774,
        "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJleHAiOjE1MzMyOTM5NjgsImlkIjoiQTEyMzQ1NiIsIm9yaWdfaWF0IjoxNTMzMjkwMzY4fQ.7O-iTJTztOaG8hnGS8NCsWIU7FVPR63SdwwX1zCkG0s"
    }

##   APP Client - refresh_token 刷新 token

GET：https://aplchat.apollogaming.net/system/refresh_token

Header：Authorization    
Value：Bearer + {{token}}

return

    {
        "code": 200,
        "expire": "2018-08-03T18:59:28+08:00",
        "id": 0,
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
      "map_user_id": 37
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
            "room_group": 1,    // 0 1v1, 1 多人群, 2 遊戲群
            "room_name": "Hi Room 5"
        },
        {
            "room_id": 21,
            "room_group": 1,
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
            "room_group": 1,    // 0 1v1, 1 多人群, 2 遊戲群
            "room_name": "room-5",
            "msg_id": 2441
        },
        {
            "room_id": 10,
            "room_group": 1,
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
      "map_user_id" 37
    }
    
return

    {
        "user_id" 37,
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
    
#  Order 信用微投

##   APP Client -  Order，UserGameSwitch  遊戲狀態
GET：https://aplchat.apollogaming.net/order/userGameSwitch

Header：Authorization    
Value：Bearer + {{token}}
    
return

    {
        "GameList": {
            "BG": {
                "BG": 350
            },
            "FastThree": {
                "BF": 338,
                "GF": 339,
                "GZ": 343,
                "HB": 342,
                "HF": 340,
                "JH": 336,
                "JL": 337,
                "KF": 345,
                "MF": 344,
                "SF": 341
            },
            "KY": {
                "KY": 351
            },
            "NormalLottery": {
                "D3": 333,
                "P5": 335,
                "PL": 334,
                "S7": 332,
                "SB": 331
            },
            "PK10": {
                "AL": 348,
                "BJ": 346,
                "QB": 347
            },
            "WanZiLottery": {
                "OZ": 349
            }
        },
        "Success": true,
        "ErrorCode": "",
        "ErrorMessage": ""
    }

##   APP Client - Order，GameIO 遊戲賠率

POST：https://aplchat.apollogaming.net/order/gameIO

Header：Authorization    
Value：Bearer + {{token}}

    {
        "GameType":"SF"
    }
    
return

    {
        "data": {
            "W1R": {
                "1": {
                    "OpenSwitch": "Y",
                    "OpenSwitchC": "Y",
                    "Ioratio": 2.005,
                    "LockIoratio": "0.000",
                    "AccIoratio": "0.000",
                    "PlayCode": "W1R",
                    "Number": 1
                },
                "2": {
                    "OpenSwitch": "Y",
                    "OpenSwitchC": "Y",
                    "Ioratio": 2.005,
                    "LockIoratio": "0.000",
                    "AccIoratio": "0.000",
                    "PlayCode": "W1R",
                    "Number": 2
                }
            },
            "WM1": {
                "RNM": {
                    "OpenSwitch": "Y",
                    "OpenSwitchC": "Y",
                    "Ioratio": 2.1,
                    "LockIoratio": "0.000",
                    "AccIoratio": "0.000",
                    "PlayCode": "RNM",
                    "Number": "RNM"
                },
                "BNM": {
                    "OpenSwitch": "Y",
                    "OpenSwitchC": "Y",
                    "Ioratio": 1.55,
                    "LockIoratio": "0.000",
                    "AccIoratio": "0.000",
                    "PlayCode": "BNM",
                    "Number": "BNM"
                }
            }
        },
        "UserInfo": {
            "Line": [
                "A",
                "B",
                "C",
                "D"
            ]
        },
        "Success": true,
         "ErrorCode": "",
         "ErrorMessage": ""
    }
    
##   APP Client - Order，GameTime 取得遊戲開關盤時間

POST：https://aplchat.apollogaming.net/order/gameTime

Header：Authorization    
Value：Bearer + {{token}}

    {
        "GameType":"SF"
    }
    
return

      {
          "data": {
              "BF": {
                  "GameID": "27466013",     //遊戲編號 (個公司的遊戲編號)
                  "GameNum": "124990",      //遊戲期數編號 (官方期數編號) 
                  "TimeType": "1",          //1:開盤, 2:關盤, 3:無期數
                  "OpenTime": "2018-11-06 16:50:00",  //開盤時間
                  "CloseTime": "2018-11-06 16:59:00", //關盤時間
                  "GameOpen": true,         //遊戲狀態 true=開放, false=關閉 
                  "CountdownTime": 470      //遊戲剩餘秒數
              }
          },
          "Success": true,
          "ErrorCode": "",
          "ErrorMessage": ""
      }

##   APP Client - Order，OrderAction 下單接口

POST：https://aplchat.apollogaming.net/order/orderAction

URL Params

    | Parameter Name | Data Category | Required | Instructions                      
    | -------------- | ------------- | -------- | -------------- 
    | UserID         | int           | Y        |                                   
    | GameType       | string        | Y        |                                   
    | GameID         | int           | Y        | 遊戲編號 (各公司的獨立遊戲編號)     
    | Line           | string        | Y        |                                   
    | Num_Str        | string        | Y        | *Ex  PlayCode@號碼@賠率@金額 , PlayCode@號碼@賠率@金額,......more  

Header：Authorization    
Value：Bearer + {{token}}

    {
        "GameType": "BF",
        "GameID": 27499058,     
        "Line": "A",
        "Num_Str": "W1R@1@20.005@10,W1R@4@2.005@9999999,W1R@5@2.005@10"
    }
    
return

      {
          "data": [
              {
                  "GameID": "27466041",
                  "PlayCode": "W1R",  //下注玩法
                  "Num": "1",         //下注號碼
                  "Msg": "賠率變動錯誤[20.005!=2.005该号赔率已变动!!]", //回傳下注結果內容
                  "IsSuccess": false  //回傳下注結果
              },
              {
                  "GameID": "27466041",
                  "PlayCode": "W1R",
                  "Num": "4",
                  "Msg": "號碼4下注9999999,超過會員單注限額=>50000",
                  "IsSuccess": false
              },
              {
                  "GameID": "27466041",
                  "PlayCode": "W1R",
                  "Num": "5",
                  "Msg": "成功",
                  "IsSuccess": true
              }
          ],
          "Success": true,
          "ErrorCode": "",
          "ErrorMessage": ""
      }
      
##   APP Client - Order，UserGameLine 取得遊戲盤口

POST：https://aplchat.apollogaming.net/order/userGameLine

Header：Authorization    
Value：Bearer + {{token}}

    {
        "GameType":"SF"
    }
    
return

      {
          "data": {
              "Line": ["A","B","C","D"]
          },
          "Success": true,
          "ErrorCode": "",
          "ErrorMessage": ""
      }
