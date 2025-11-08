{
  "name": "🎬 Instantly Turn Ideas into Viral Instagram Reel Scenarios 🤖 (Telegram, AI Agent)",
  "nodes": [
    {
      "parameters": {
        "updates": [
          "message"
        ],
        "additionalFields": {}
      },
      "name": "Start: Receive Message on Telegram",
      "type": "n8n-nodes-base.telegramTrigger",
      "position": [
        224,
        464
      ],
      "webhookId": "24724bcc-67fa-442f-a2d7-d1d62683ce31",
      "typeVersion": 1.1,
      "id": "10c98770-a77c-4aaa-a738-aee4c9d81273",
      "credentials": {
        "telegramApi": {
          "id": "bXInYqWmbrJHLl0P",
          "name": "Telegram account"
        }
      }
    },
    {
      "parameters": {
        "model": {
          "__rl": true,
          "mode": "list",
          "value": "gpt-4o",
          "cachedResultName": "gpt-4o"
        },
        "options": {}
      },
      "name": "AI Model: GPT-4o",
      "type": "@n8n/n8n-nodes-langchain.lmChatOpenAi",
      "position": [
        1088,
        592
      ],
      "typeVersion": 1.2,
      "id": "a6cf7840-0199-4f56-9e1b-f9043f21c1f3"
    },
    {
      "parameters": {
        "sessionIdType": "customKey",
        "sessionKey": "={{ $('Start: Receive Message on Telegram').item.json.message.chat.id }}",
        "contextWindowLength": 10
      },
      "name": "Memory for Chat Context",
      "type": "@n8n/n8n-nodes-langchain.memoryBufferWindow",
      "position": [
        1248,
        592
      ],
      "typeVersion": 1.3,
      "id": "10af547d-c245-4abf-b9bf-223a91b6337a"
    },
    {
      "parameters": {
        "operation": "append",
        "documentId": {
          "__rl": true,
          "mode": "id",
          "value": ""
        },
        "sheetName": {
          "__rl": true,
          "mode": "list",
          "value": ""
        }
      },
      "name": "Optional: Log Ideas to Google Sheets",
      "type": "n8n-nodes-base.googleSheetsTool",
      "position": [
        1408,
        592
      ],
      "typeVersion": 4.5,
      "id": "7e16099d-c057-4300-a172-85b847ef79d1",
      "disabled": true
    },
    {
      "parameters": {
        "assignments": {
          "assignments": [
            {
              "name": "Error",
              "type": "string",
              "value": "An error has occurred"
            }
          ]
        },
        "options": {}
      },
      "name": "Set Error Message",
      "type": "n8n-nodes-base.set",
      "position": [
        672,
        672
      ],
      "typeVersion": 3.4,
      "id": "b7fe6abd-a7cf-438f-b6d9-84aa1712e6b2"
    },
    {
      "parameters": {
        "promptType": "define",
        "text": "={{ $json.text }}",
        "options": {
          "systemMessage": "=You are a marketing expert with 25 years of experience.\nYou studied under the best U.S. marketers and copywriters—Russell Brunson, Dan Kennedy, Gary Halbert, Alex Hormozi, Todd Brown, and others.\n\nYou also master viral Instagram Reels that rack up millions of views.\nYou know exactly how to grab and hold attention using top-tier marketing and psychology methods.\nYou command emotional storytelling and leverage psychological influence principles, blending brilliant techniques from legends such as Gary Bencivenga, Joe Sugarman, Dan Kennedy, Chris Haddad, John Carlton, David Ogilvy, Seth Godin, and more.\n\nWork at full power—it's extremely important to me to get the best possible result.\n\nYou write hooks no one can scroll past.\n\nWrite in simple, lively language—as if speaking straight into the camera.\nAvoid complicated wording, \"info-style\" delivery, and templates.\nShort sentences, spoken tone, no \"As an expert, I think…,\" no fluff.\nImagine the person records this Reel in one take—emotional, with rhythm, pauses, energy.\n\nBelow you'll find the idea for the Reel (transcript of the user's voice note):\n\n\"{text}\"\n\nBased on this, create:\n\t1.\tA Reel script (30–60 seconds) in the format:\n• HOOK — eye-catching first line\n• SUBTITLE — amplifies curiosity & value promise\n• BODY — explanation / story / argument / core message\n• CTA — light, non-generic call to action\n\t2.\tThree hook variants—no clichés, no emojis, but designed to stand out in the timeline\n\t3.\tA short Reel caption (1–2 lines)—to appear under the Reel\n\n❗ Important: The viewer has already watched the Reel and is now reading the caption.\nYour job: keep their attention, trigger an \"aha\" moment, or spark the desire to save/share.\n\nThe caption should\n– be easy to understand\n– avoid repeating lines from the video\n– strengthen the Reel's core message\n– motivate an internal reaction or action\n\nExample openings:\n— \"And here's what almost every expert overlooks…\"\n— \"Don't forget this before your next Reel post\"\n— \"Ever experienced this too?\"\n\n❌ Avoid clichés like \"Hey guys,\" \"Watch until the end,\" \"Subscribe to my channel.\"\n\n📸 Additional task – VISUAL IDEA for the Reel\nBased on the content, tone, and mood, give 1–2 concrete recommendations for suitable footage or imagery.\nThe visual idea should support the hook, amplify the emotion, and captivate the viewer within the first 2 seconds.\n\nNo generic suggestions like \"just show yourself on camera.\" Think concrete and cinematic:\n– Exactly what should be visible?\n– What happens in the background?\n– How's the lighting / mood?\n– Any visual metaphor or strong movement?\n\nExamples:\n— \"Dark room, only the face in focus, emotional close-up, camera slowly moving toward the person\"\n— \"Cut between old Insta posts and the person staring seriously into the lens—then switch to a smiling face\"\n— \"Smartphone angrily tossed aside, then close-up of a calm, confident face delivering the message\"\n\n📦 Return the result in this format:\n\n⸻\n\n💡 Hook (variants):\n\t1.\t…\n\t2.\t…\n\t3.\t…\n\n🎬 Script:\n• Hook: …\n• Subtitle: …\n• Body: …\n• CTA: …\n\n📝 Reel Caption:\n…\n\n📸 Visual Idea:\n…"
        }
      },
      "name": "Generate Reels Scenario with AI",
      "type": "@n8n/n8n-nodes-langchain.agent",
      "position": [
        1136,
        368
      ],
      "typeVersion": 1.8,
      "id": "91de9f84-298f-4b78-95be-c49e7615e777"
    },
    {
      "parameters": {
        "chatId": "={{ $('Start: Receive Message on Telegram').item.json.message.chat.id }}",
        "text": "={{ $json.output }}",
        "additionalFields": {
          "appendAttribution": false
        }
      },
      "name": "Send Scenario to Telegram",
      "type": "n8n-nodes-base.telegram",
      "position": [
        1552,
        368
      ],
      "webhookId": "7128ba1f-5668-4ea5-9d9d-1c8bcb424d1d",
      "typeVersion": 1.2,
      "id": "fd269346-022f-443e-b8a7-ab76292e567d",
      "credentials": {
        "telegramApi": {
          "id": "bXInYqWmbrJHLl0P",
          "name": "Telegram account"
        }
      }
    },
    {
      "parameters": {
        "rules": {
          "values": [
            {
              "conditions": {
                "options": {
                  "version": 2,
                  "leftValue": "",
                  "caseSensitive": true,
                  "typeValidation": "strict"
                },
                "combinator": "and",
                "conditions": [
                  {
                    "operator": {
                      "type": "string",
                      "operation": "exists",
                      "singleValue": true
                    },
                    "leftValue": "={{ $json.message.voice.file_id }}",
                    "rightValue": ""
                  }
                ]
              },
              "renameOutput": true,
              "outputKey": "Audio"
            },
            {
              "conditions": {
                "options": {
                  "version": 2,
                  "leftValue": "",
                  "caseSensitive": true,
                  "typeValidation": "strict"
                },
                "combinator": "and",
                "conditions": [
                  {
                    "operator": {
                      "type": "string",
                      "operation": "exists",
                      "singleValue": true
                    },
                    "leftValue": "={{ $json.message.text || \"\" }}",
                    "rightValue": ""
                  }
                ]
              },
              "renameOutput": true,
              "outputKey": "Text"
            },
            {
              "conditions": {
                "options": {
                  "version": 2,
                  "leftValue": "",
                  "caseSensitive": true,
                  "typeValidation": "strict"
                },
                "combinator": "and",
                "conditions": [
                  {
                    "operator": {
                      "type": "string",
                      "operation": "exists",
                      "singleValue": true
                    },
                    "leftValue": "error",
                    "rightValue": ""
                  }
                ]
              },
              "renameOutput": true,
              "outputKey": "Error"
            }
          ]
        },
        "options": {}
      },
      "name": "Route by Input Type",
      "type": "n8n-nodes-base.switch",
      "position": [
        448,
        464
      ],
      "typeVersion": 3.2,
      "id": "c64ed3de-f6db-4677-bd04-83ecef0a61e7"
    },
    {
      "parameters": {
        "assignments": {
          "assignments": [
            {
              "name": "text",
              "type": "string",
              "value": "={{ $json.message.text }}"
            }
          ]
        },
        "options": {}
      },
      "name": "Set User Input",
      "type": "n8n-nodes-base.set",
      "position": [
        880,
        464
      ],
      "typeVersion": 3.4,
      "id": "f414bfde-0904-4565-9ed5-7355e7bc9ec5"
    },
    {
      "parameters": {
        "chatId": "={{ $('Start: Receive Message on Telegram').item.json.message.chat.id }}",
        "text": "={{ $json.output }}",
        "additionalFields": {
          "appendAttribution": false
        }
      },
      "name": "Send Error Message to Telegram",
      "type": "n8n-nodes-base.telegram",
      "position": [
        880,
        672
      ],
      "webhookId": "be00367f-17a9-4ec0-b624-cf724c3308f1",
      "typeVersion": 1.2,
      "id": "71ef1d6a-279e-4b05-ad6b-4a916be4a949",
      "credentials": {
        "telegramApi": {
          "id": "bXInYqWmbrJHLl0P",
          "name": "Telegram account"
        }
      }
    },
    {
      "parameters": {
        "resource": "file",
        "fileId": "={{ $json.message.voice.file_id }}",
        "additionalFields": {}
      },
      "name": "Get Voice Message",
      "type": "n8n-nodes-base.telegram",
      "position": [
        672,
        272
      ],
      "webhookId": "6ae3704e-7510-4c91-9381-2dae5577a287",
      "typeVersion": 1.2,
      "id": "147c05c3-7fa4-4802-acf0-ce5b5e7b622e",
      "credentials": {
        "telegramApi": {
          "id": "bXInYqWmbrJHLl0P",
          "name": "Telegram account"
        }
      }
    },
    {
      "parameters": {
        "resource": "audio",
        "operation": "transcribe",
        "options": {}
      },
      "name": "Transcribe Voice to Text",
      "type": "@n8n/n8n-nodes-langchain.openAi",
      "position": [
        880,
        272
      ],
      "typeVersion": 1.8,
      "id": "1bf5c02d-b647-470a-a36b-d755feaf678a"
    }
  ],
  "pinData": {},
  "connections": {
    "Set User Input": {
      "main": [
        [
          {
            "node": "Generate Reels Scenario with AI",
            "type": "main",
            "index": 0
          }
        ]
      ]
    },
    "AI Model: GPT-4o": {
      "ai_languageModel": [
        [
          {
            "node": "Generate Reels Scenario with AI",
            "type": "ai_languageModel",
            "index": 0
          }
        ]
      ]
    },
    "Get Voice Message": {
      "main": [
        [
          {
            "node": "Transcribe Voice to Text",
            "type": "main",
            "index": 0
          }
        ]
      ]
    },
    "Set Error Message": {
      "main": [
        [
          {
            "node": "Send Error Message to Telegram",
            "type": "main",
            "index": 0
          }
        ]
      ]
    },
    "Route by Input Type": {
      "main": [
        [
          {
            "node": "Get Voice Message",
            "type": "main",
            "index": 0
          }
        ],
        [
          {
            "node": "Set User Input",
            "type": "main",
            "index": 0
          }
        ],
        [
          {
            "node": "Set Error Message",
            "type": "main",
            "index": 0
          }
        ]
      ]
    },
    "Memory for Chat Context": {
      "ai_memory": [
        [
          {
            "node": "Generate Reels Scenario with AI",
            "type": "ai_memory",
            "index": 0
          }
        ]
      ]
    },
    "Transcribe Voice to Text": {
      "main": [
        [
          {
            "node": "Generate Reels Scenario with AI",
            "type": "main",
            "index": 0
          }
        ]
      ]
    },
    "Generate Reels Scenario with AI": {
      "main": [
        [
          {
            "node": "Send Scenario to Telegram",
            "type": "main",
            "index": 0
          }
        ]
      ]
    },
    "Start: Receive Message on Telegram": {
      "main": [
        [
          {
            "node": "Route by Input Type",
            "type": "main",
            "index": 0
          }
        ]
      ]
    },
    "Optional: Log Ideas to Google Sheets": {
      "ai_tool": [
        [
          {
            "node": "Generate Reels Scenario with AI",
            "type": "ai_tool",
            "index": 0
          }
        ]
      ]
    }
  },
  "active": false,
  "settings": {
    "executionOrder": "v1"
  },
  "versionId": "ca169fb1-14e9-4454-b240-1bd4525b9132",
  "meta": {
    "instanceId": "3f8a7ff04bfdf4e4fb5a688567e5d5388bccb52782292b712b8dc6c8823956b2"
  },
  "id": "AY71TPw81CUhPWHe",
  "tags": []
}
