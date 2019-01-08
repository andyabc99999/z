# 使用者
				
##   APP Client - user Login 使用者登入

POST：https://aplchat.apollogaming.net/user/login

Header：Content-Type     
Value：application/json

    {
      "username": "chatroom12",
      "password": "aa123456",
      "tpl":"dio999",
      "app_type": 1,
      "app_token": "d0516a8e71ad875b0243b753ed5f0ccba27389e6e90b4bf8e993cb22e27cbe68"
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
##   APP Client - get message from stream (SSE) 讀取頻道訊息

listen：https://aplchat.apollogaming.net/chat/stream  

Header：Authorization    
Value：Bearer + {{token}}

##   APP Client - broken SSE line 使用者主動斷開SSE連線

GET：https://aplchat.apollogaming.net/chat/break  

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

##   APP Client -  Order，UserGameSwitch  遊戲狀態，取得會員遊戲開關 / 各遊戲盤口
GET：https://aplchat.apollogaming.net/order/userGameSwitch

Header：Authorization    
Value：Bearer + {{token}}
    
* **return**

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

* **Error Response:**

    Code: 403 Forbidden
  
      {
          "Success": false,
          "ErrorCode": "00009",
          "ErrorMessage": "找不到登入记录,请重新登入!!"
      }

##   APP Client - Order，GameIO 遊戲賠率

POST：https://aplchat.apollogaming.net/order/gameIO

Header：Authorization    
Value：Bearer + {{token}}

* **URL Params**  

    |Parameter Name | Data Category | Required | Instructions |
    | -------------- | ------------- | -------- | ------------ |
    | GameType       | string        | Y        | about...     |

* **send**

        {
            "GameType":"SF"
        }
        
* **return**

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

* **Error Response:**

    Code: 403 Forbidden
  
      {
          "Success": false,
          "ErrorCode": "00009",
          "ErrorMessage": "找不到登入记录,请重新登入!!"
      }

##   APP Client - Order，GameTime 取得遊戲開關盤時間

POST：https://aplchat.apollogaming.net/order/gameTime

Header：Authorization    
Value：Bearer + {{token}}

* **URL Params**  

    | Parameter Name | Data Category | Required | Instructions |
    | -------------- | ------------- | -------- | ------------ |
    | UserID         | int           | Y        |              |
    | GameType       | string        | N        | 傳入GameCode (不傳預設回傳全部遊戲開關盤時間)     |
    
* **send**

        {
            "GameType":"SF"
        }
        
* **return**

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

Header：Authorization    
Value：Bearer + {{token}}

* **URL Params**  

    | Parameter Name | Data Category | Required | Instructions                      
    | -------------- | ------------- | -------- | --------------                       
    | GameType       | string        | Y        |                                   
    | GameID         | int           | Y        | 遊戲編號 (各公司的獨立遊戲編號)     
    | Line           | string        | Y        |                                   
    | Num_Str        | string        | Y        | *Ex  PlayCode@號碼@賠率@金額 , PlayCode@號碼@賠率@金額,......more  

* **send**

        {
            "GameType": "BF",
            "GameID": 27499058,     
            "Line": "A",
            "Num_Str": "W1R@1@20.005@10,W1R@4@2.005@9999999,W1R@5@2.005@10"
        }
    
* **return**

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

* **Error Response:**

    Code: 403 Forbidden
  
        {
            "Success": false,
            "ErrorCode": "00024",
            "ErrorMessage": "游戏期数已关闭"
        }
      
##   APP Client - Order，UserGameLine 取得遊戲盤口

POST：https://aplchat.apollogaming.net/order/userGameLine

Header：Authorization    
Value：Bearer + {{token}}

* **URL Params**  

    | Parameter Name | Data Category | Required | Instructions |
    | -------------- | ------------- | -------- | ------------ |
    | GameType       | string        | Y        |              |   

* **send**

       {
           "GameType":"SF"
       }
    
* **return**

      {
          "data": {
              "Line": ["A","B","C","D"]
          },
          "Success": true,
          "ErrorCode": "",
          "ErrorMessage": ""
      }

* **Error Response:**

    Code: 403 Forbidden
  
        {
            "Success": false,
            "ErrorCode": "00435",
            "ErrorMessage": "游戏参数错误!!"
        }
      
##   APP Client - Order，UserCash  取得會員額度

POST：https://aplchat.apollogaming.net/order/userCash

Header：Authorization    
Value：Bearer + {{token}}

* **URL Params**  

    | Parameter Name | Data Category | Required | Instructions |
    | -------------- | ------------- | -------- | ------------ |
    | GameType       | string        | Y        | 可傳GameCode 回傳該遊戲額度,或傳入"All" 取得該會員所有額度       |

* **send**

        {
            "GameType":"SF"
        }
    
* **return**

        {
            "data": {
                "AllCash": {
                    "Cash": "1000000",
                    "P5": "1000000",
                    "S7": "1000000",
                    "SB": "1000000"
                }
            },
            "Success": true,
            "ErrorCode": "",
            "ErrorMessage": ""
        }

* **Error Response:**

    Code: 403 Forbidden
  
        {
            "Success": false,
            "ErrorCode": "00435",
            "ErrorMessage": "游戏参数错误!!"
        }    
    
##   APP Client - Order，WagersDayReport  取得會員日報表

POST：https://aplchat.apollogaming.net/order/wagersDayReport

Header：Authorization    
Value：Bearer + {{token}}

* **URL Params**  

    | Parameter Name | Data Category | Required | Instructions |
    | -------------- | ------------- | -------- | ------------ |
    | GameType       | string        | Y        | 可傳GameCode 回傳該遊戲額度,或傳入"All" 取得該會員所有額度       |

* **回傳參數**

    | Parameter Name | Data Category | Instructions     |
    | -------------- | ------------- | ---------------- |
    | sum            |               |                  |
    | Gold           | float         | 注單下注金額總計 |
    | Nums           | int           | 注單量總計       |
    | WinGold        | float         | 注單派彩金額總計 |
    | Reba           | float         | 注單退水金額總計 |
    | data           |               |                  |
    | AccountDate    | date          | 日期             |
    | AccountWeek    | string        | 星期             |
    | Nums           | string        | 注單量           |
    | Gold           | string        | 注單下注金額總計 |
    | WinGold        | string        | 注單派彩金額總計 |
    | Reba           | string        | 注單退水金額總計 |


* **send**

        {
            "GameType":"SF"
        }
    
* **return**

        //單一遊戲
        {    
            "FastThree": {
                "JH": {
                    "data": {
                        "2018-12-29": {
                            "AccountDate": "2018-12-29",
                            "AccountWeek": "六",
                            "Nums": "5",
                            "Gold": "100",
                            "WinGold": "78.880",
                            "Reba": "2.6000"
                        },
                        "2018-12-23": {
                            "AccountDate": "2018-12-23",
                            "AccountWeek": "日",
                            "Nums": "8",
                            "Gold": "83",
                            "WinGold": "90.720",
                            "Reba": "3.9300"
                        }
                    },
                    "sum": {
                        "Gold": 183,
                        "Nums": 13,
                        "WinGold": 169.6,
                        "Reba": 6.53
                    }
                }
            },
            "Success": true,
            "ErrorCode": "",
            "ErrorMessage": ""
        }
        
        //單一遊戲 (無注單資料回傳)
        {   
            "FastThree": {
                "JL": {
                    "data": false,
                    "sum": false
                }
            },
            "Success": true,
            "ErrorCode": "",
            "ErrorMessage": ""
        }
        
        //全部遊戲 (All) 
        {   
            "FastThree": {
                "JH": {
                    "sum": {
                        "Gold": 183,
                        "Nums": 13,
                        "WinGold": 169.6,
                        "Reba": 6.53
                    },
                    "data": {
                        "2018-12-29": {
                            "AccountDate": "2018-12-29",
                            "AccountWeek": "六",
                            "Nums": "5",
                            "Gold": "100",
                            "WinGold": "78.880",
                            "Reba": "2.6000"
                        },
                        "2018-12-23": {
                            "AccountDate": "2018-12-23",
                            "AccountWeek": "日",
                            "Nums": "8",
                            "Gold": "83",
                            "WinGold": "90.720",
                            "Reba": "3.9300"
                        }
                    }
                }
            },
            "PK10": {
                "BJ": {
                    "data": {
                        "2018-12-28": {
                            "AccountDate": "2018-12-28",
                            "AccountWeek": "五",
                            "Nums": "2",
                            "Gold": "20",
                            "WinGold": "19.400",
                            "Reba": "0.5000"
                        },
                        "2018-12-23": {
                            "AccountDate": "2018-12-23",
                            "AccountWeek": "日",
                            "Nums": "4",
                            "Gold": "40",
                            "WinGold": "18.400",
                            "Reba": "1.0000"
                        }
                    },
                    "sum": {
                        "Gold": 60,
                        "Nums": 6,
                        "WinGold": 37.8,
                        "Reba": 1.5
                    }
                },
                "QB": {
                    "data": {
                        "2018-12-23": {
                            "AccountDate": "2018-12-23",
                            "AccountWeek": "日",
                            "Nums": "10",
                            "Gold": "100",
                            "WinGold": "58.200",
                            "Reba": "2.0000"
                        }
                    },
                    "sum": {
                        "Gold": 100,
                        "Nums": 10,
                        "WinGold": 58.2,
                        "Reba": 2
                    }
                }
            },
            "Success": true,
            "ErrorCode": "",
            "ErrorMessage": ""
        }
        
        //全部遊戲無注單回傳_1
        {   
            "FastThree": {
                "JH": {
                    "sum": {
                        "Gold": 10,
                        "Nums": 1,
                        "WinGold": 0,
                        "Reba": 1
                    },
                    "data": {
                        "2018-12-29": {
                            "AccountDate": "2018-12-29",
                            "AccountWeek": "六",
                            "Nums": "1",
                            "Gold": "10",
                            "WinGold": "0.000",
                            "Reba": "1.0000"
                        }
                    }
                }
            },
            "PK10": false,
            "Success": true,
            "ErrorCode": "",
            "ErrorMessage": ""
        }
        
        //全部遊戲無注單回傳_2
         {   
                    "FastThree": false,
                    "PK10": false,
            "Success": true,
            "ErrorCode": "",
            "ErrorMessage": ""
         }

* **Error Response:**

    Code: 403 Forbidden
  
        {
            "Success": false,
            "ErrorCode": "00435",
            "ErrorMessage": "游戏参数错误!!"
        }
         
##   APP Client - Order，WagersHistory  取得會員詳細投注紀錄

POST：https://aplchat.apollogaming.net/order/wagersHistory

Header：Authorization    
Value：Bearer + {{token}}

* **URL Params**  

    | Parameter Name | Data Category | Required | Instructions |
    | -------------- | ------------- | -------- | ------------ |
    | UserID         | int           | Y        | about...     |
    | GameType       | string        | Y        | GameCode     |
    | Date           | date          | Y        | "2018-12-31" |
    | Page           | int           | N        | 預設第一頁   |

* **回傳參數**

    | Parameter Name | Data Category | Instructions               |    
    | -------------- | ------------- | -------------------------- |
    | WagersID       | string        | 母單編號                   |
    | WagersSubID    | string        | 子單編號                   |
    | Line           | string        | 盤口                       |
    | GameID         | string        | 遊戲編號                   |
    | GameNum        | string        | 遊戲期數                   |
    | Ioratio        | string        | 賠率                       |
    | PlayCode       | string        | 下注遊戲內容代碼           |
    | Number         | string        | 下注遊戲內容號碼           |
    | Gold           | string        | 下注金額                   |
    | WinLossGold    | string        | 損益金額                   |
    | WinGold        | string        | 派彩金額                   |
    | Result         | string        | 開獎狀態 W=贏,L=輸,N=平局  |
    | Status         | string        | 注單狀態 1=正常單  2=註銷單 3=回復單&註銷單的補單 |
    | TraceNum       | string        | 追號單(可先忽略)           |
    | BetTime        | string        | 下注時間                   |
    | RebaMEM        | string        | 退水                       |    
    | GameReslutStr  | string        | 開獎結果                   |
    | SumGold        | string        | 當頁下注金總計             |
    | SumReba        | string        | 當頁退水金總計             |
    | SumWinLoss     | string        | 當頁輸贏金總計             |
    | TotalNums      | string        | 資料總比數                 |
    | TotalPages     | string        | 總頁數                     |
    | NowPage        | string        | 當頁數                     |


* **send**

        {
            "UserID": 515849,
            "GameType": "BF",
            "Date": "2018-12-31",
            "Page": 1
        }
    
* **return**

         {
                    "data": [
                        {
                            "WagersID": "26873",
                            "WagersSubID": "44259",
                            "Line": "A",
                            "GameID": "28349183",
                            "GameNum": "181229072",
                            "Ioratio": "1.972",
                            "PlayCode": "W321V",
                            "Number": "S",
                            "Gold": "20",
                            "WinLossGold": "19.64",
                            "WinGold": "39.440",
                            "Result": "W",
                            "Status": "1",
                            "TraceNum": "N",
                            "BetTime": [
                                "2018-12-29",
                                "20:26:33"
                            ],
                            "RebaMEM": "0.2",
                            "GameReslutStr": "S"
                        },
                        {
                            "WagersID": "26872",
                            "WagersSubID": "44258",
                            "Line": "A",
                            "GameID": "28349183",
                            "GameNum": "181229072",
                            "Ioratio": "3.000",
                            "PlayCode": "TSE",
                            "Number": "S",
                            "Gold": "20",
                            "WinLossGold": "-19",
                            "WinGold": "0.000",
                            "Result": "L",
                            "Status": "1",
                            "TraceNum": "N",
                            "BetTime": [
                                "2018-12-29",
                                "20:26:33"
                            ],
                        "RebaMEM": "1",
                        "GameReslutStr": "TSD"
                    },
                    {
                        "WagersID": "26871",
                        "WagersSubID": "44257",
                        "Line": "A",
                        "GameID": "28349183",
                        "GameNum": "181229072",
                        "Ioratio": "3.000",
                        "PlayCode": "TBD",
                        "Number": "B",
                        "Gold": "20",
                        "WinLossGold": "-19",
                        "WinGold": "0.000",
                        "Result": "L",
                        "Status": "1",
                        "TraceNum": "N",
                        "BetTime": [
                            "2018-12-29",
                            "20:26:33"
                        ],
                        "RebaMEM": "1",
                        "GameReslutStr": "TSD"
                    },
                    {
                        "WagersID": "26870",
                        "WagersSubID": "44256",
                        "Line": "A",
                        "GameID": "28349183",
                        "GameNum": "181229072",
                        "Ioratio": "1.972",
                        "PlayCode": "W321T",
                        "Number": "D",
                        "Gold": "20",
                        "WinLossGold": "19.64",
                        "WinGold": "39.440",
                        "Result": "W",
                        "Status": "1",
                        "TraceNum": "N",
                        "BetTime": [
                            "2018-12-29",
                            "20:26:33"
                        ],
                        "RebaMEM": "0.2",
                        "GameReslutStr": "D"
                    },
                    {
                        "WagersID": "26870",
                        "WagersSubID": "44255",
                        "Line": "A",
                        "GameID": "28349183",
                        "GameNum": "181229072",
                        "Ioratio": "1.972",
                        "PlayCode": "W321T",
                        "Number": "E",
                        "Gold": "20",
                        "WinLossGold": "-19.8",
                        "WinGold": "0.000",
                        "Result": "L",
                        "Status": "1",
                        "TraceNum": "N",
                        "BetTime": [
                            "2018-12-29",
                            "20:26:33"
                        ],
                        "RebaMEM": "0.2",
                        "GameReslutStr": "D"
                    }
                ],
                "Total": {
                    "SumGold": "100",
                    "SumReba": "2.6",
                    "SumWinLoss": "-18.52"
                },
                "PageInfo": {
                    "TotalNums": "5",
                    "TotalPages": "1",
                    "NowPage": "1"
                },
                "Success": true,
                "ErrorCode": "",
                "ErrorMessage": ""
            }
            
* **Error Response:**

    Code: 403 Forbidden
  
        {
            "Success": false,
            "ErrorCode": "00435",
            "ErrorMessage": "游戏参数错误!!"
        }
