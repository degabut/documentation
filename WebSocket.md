# Degabut WebSocket Documentation

Notes:

- Received / sent message format will always be JSON with `event` (`string`) and `data` (`object`, `array`, or `null`) key, for example:

```json
{
  "event": "identify",
  "data": {
    "token": "your-token"
  }
}
```

- The client expected to send the [`identify`](#identify) message within **5 seconds** after being connected. If identification failed (invalid token / timed out), the server will automatically close the connection
- [`player-tick`](#player-tick) event will be emitted everytime Lavalink sends `playerUpdate` event, if you are using the [official example](https://github.com/degabut/examples/tree/main/v3), this event will be emitted every second when there's something playing on the queue

Other than that, the event list below should be self-explanatory

## Table of Contents

- [Send](#send)
  - [Identify](#identify)
- [Receive](#receive)
  - [Identify](#identify)
  - [Queue Created](#queue-created)
  - [Queue Destroyed](#queue-destroyed)
  - [Queue Joined / Left](#queue-joined--left)
  - [Queue Loop Mode Changed](#queue-loop-mode-changed)
  - [Queue Shuffle Toggled](#queue-shuffle-toggled)
  - [Queue Cleared](#queue-cleared)
  - [Queue Processed](#queue-processed)
  - [Queue Text Channel Changed](#queue-text-channel-changed)
  - [Member Joined / Removed / Updated](#member-joined--removed--updated)
  - [Member Jammed](#member-jammed)
  - [Player Pause State Changed](#player-pause-state-changed)
  - [Player Tick](#player-tick)
  - [Track Added / Removed / Skipped](#track-added--removed--skipped)
  - [Track Order Changed](#track-order-changed)
  - [Track Seeked](#track-seeked)
  - [Track Audio Started](#track-audio-started)
  - [Tracks Added / Removed](#tracks-added--removed)

## Send

List of messages that you can send with its payload

### Identify

```json
{
  "event": "identify",
  "data": {
    "token": "{{token}}"
  }
}
```

## Receive

List of possible messages received and its payload

### Identify

```json
{
  "event": "identify",
  "data": {
    "userId": "294448191808602112"
  }
}
```

### Queue Created

```json
{
  "event": "queue-created",
  "data": {
    "tracks": [],
    "history": [],
    "nowPlaying": null,
    "autoplay": false,
    "shuffle": false,
    "loopType": "DISABLED",
    "voiceChannel": {
      "id": "954618520560361516",
      "name": "General",
      "members": [
        {
          "id": "294448191808602112",
          "displayName": "Owl",
          "nickname": "Owl",
          "username": "Owl",
          "discriminator": "9652",
          "avatar": "https://cdn.discordapp.com/avatars/294448191808602112/ebca542afbac6f67bdd0bc776a16ad0c.webp"
        },
        {
          "id": "955855161694228500",
          "displayName": "Gabut.spec.js",
          "nickname": null,
          "username": "Gabut.spec.js",
          "discriminator": "2989",
          "avatar": null
        }
      ]
    }
  }
}
```

### Queue Destroyed

```json
{
  "event": "queue-destroyed",
  "data": {}
}
```

### Queue Joined / Left

```json
{
  "event": "queue-joined", // queue-joined | queue-left
  "data": {
    "voiceChannelId": "954618520560361516"
  }
}
```

### Queue Loop Mode Changed

```json
{
  "event": "queue-loop-mode-changed",
  "data": {
    "loopMode": "DISABLED" // DISABLED | TRACK | QUEUE
  }
}
```

### Queue Shuffle Toggled

```json
{
  "event": "queue-shuffle-toggled",
  "data": {
    "shuffle": true
  }
}
```

### Queue Cleared

```json
{
  "event": "queue-cleared",
  "data": {
    "tracks": [
      // tracks left on queue, empty array if inclueNowPlaying is true when clearing queue
      {
        "id": "d5ceffe2-0c23-42ae-ab7b-305151637da3",
        "url": "https://youtu.be/_N6vSc_mT6I",
        "video": {
          "id": "_N6vSc_mT6I",
          "title": "TULUS - Hati-Hati di Jalan (Official Lyric Video)",
          "duration": 243,
          "thumbnails": [
            {
              "url": "https://i.ytimg.com/vi/_N6vSc_mT6I/hq720.jpg?sqp=-oaymwEjCOgCEMoBSFryq4qpAxUIARUAAAAAGAElAADIQj0AgKJDeAE=&rs=AOn4CLAGYEmBYZ98p0-W89nqc49HVqSrSg",
              "width": 360,
              "height": 202
            },
            {
              "url": "https://i.ytimg.com/vi/_N6vSc_mT6I/hq720.jpg?sqp=-oaymwEXCNAFEJQDSFryq4qpAwkIARUAAIhCGAE=&rs=AOn4CLBxA7gSFlYzGrkzskQZr2WGywyuig",
              "width": 720,
              "height": 404
            }
          ],
          "viewCount": "100450942",
          "channel": {
            "id": "UCRggxhdYIz0zSvUgJmCWMGg",
            "name": "Tulus",
            "thumbnails": [
              {
                "url": "https://yt3.ggpht.com/y4zoHuQG2_ZulwkfGZ0CCFNf9C-49XPB9eKDSepPNigzZ_1RRaWADFcY8OD1S6zNuXmWh2ypAA=s48-c-k-c0x00ffffff-no-nd-rj",
                "width": 48,
                "height": 48
              },
              {
                "url": "https://yt3.ggpht.com/y4zoHuQG2_ZulwkfGZ0CCFNf9C-49XPB9eKDSepPNigzZ_1RRaWADFcY8OD1S6zNuXmWh2ypAA=s88-c-k-c0x00ffffff-no-nd-rj",
                "width": 88,
                "height": 88
              },
              {
                "url": "https://yt3.ggpht.com/y4zoHuQG2_ZulwkfGZ0CCFNf9C-49XPB9eKDSepPNigzZ_1RRaWADFcY8OD1S6zNuXmWh2ypAA=s176-c-k-c0x00ffffff-no-nd-rj",
                "width": 176,
                "height": 176
              }
            ]
          }
        },
        "requestedBy": {
          "id": "294448191808602112",
          "displayName": "Owl",
          "nickname": null,
          "username": "Owl",
          "discriminator": "9652",
          "avatar": "https://cdn.discordapp.com/avatars/294448191808602112/1065d499bca0e0272fe60d397f8c6c95.webp"
        },
        "playedAt": null
      }
    ],
    "member": {
      "id": "294448191808602112",
      "displayName": "Owl",
      "nickname": null,
      "username": "Owl",
      "discriminator": "9652",
      "avatar": "https://cdn.discordapp.com/avatars/294448191808602112/1065d499bca0e0272fe60d397f8c6c95.webp"
    }
  }
}
```

### Queue Processed

```json
{
  "event": "queue-processed",
  "data": {
    // can be null if queue is processed but no tracks left on queue
    "id": "d5ceffe2-0c23-42ae-ab7b-305151637da3",
    "url": "https://youtu.be/_N6vSc_mT6I",
    "video": {
      "id": "_N6vSc_mT6I",
      "title": "TULUS - Hati-Hati di Jalan (Official Lyric Video)",
      "duration": 243,
      "thumbnails": [
        {
          "url": "https://i.ytimg.com/vi/_N6vSc_mT6I/hq720.jpg?sqp=-oaymwEjCOgCEMoBSFryq4qpAxUIARUAAAAAGAElAADIQj0AgKJDeAE=&rs=AOn4CLAGYEmBYZ98p0-W89nqc49HVqSrSg",
          "width": 360,
          "height": 202
        },
        {
          "url": "https://i.ytimg.com/vi/_N6vSc_mT6I/hq720.jpg?sqp=-oaymwEXCNAFEJQDSFryq4qpAwkIARUAAIhCGAE=&rs=AOn4CLBxA7gSFlYzGrkzskQZr2WGywyuig",
          "width": 720,
          "height": 404
        }
      ],
      "viewCount": "100450942",
      "channel": {
        "id": "UCRggxhdYIz0zSvUgJmCWMGg",
        "name": "Tulus",
        "thumbnails": [
          {
            "url": "https://yt3.ggpht.com/y4zoHuQG2_ZulwkfGZ0CCFNf9C-49XPB9eKDSepPNigzZ_1RRaWADFcY8OD1S6zNuXmWh2ypAA=s48-c-k-c0x00ffffff-no-nd-rj",
            "width": 48,
            "height": 48
          },
          {
            "url": "https://yt3.ggpht.com/y4zoHuQG2_ZulwkfGZ0CCFNf9C-49XPB9eKDSepPNigzZ_1RRaWADFcY8OD1S6zNuXmWh2ypAA=s88-c-k-c0x00ffffff-no-nd-rj",
            "width": 88,
            "height": 88
          },
          {
            "url": "https://yt3.ggpht.com/y4zoHuQG2_ZulwkfGZ0CCFNf9C-49XPB9eKDSepPNigzZ_1RRaWADFcY8OD1S6zNuXmWh2ypAA=s176-c-k-c0x00ffffff-no-nd-rj",
            "width": 176,
            "height": 176
          }
        ]
      }
    },
    "requestedBy": {
      "id": "294448191808602112",
      "displayName": "Owl",
      "nickname": null,
      "username": "Owl",
      "discriminator": "9652",
      "avatar": "https://cdn.discordapp.com/avatars/294448191808602112/1065d499bca0e0272fe60d397f8c6c95.webp"
    },
    "playedAt": null
  }
}
```


### Queue Text Channel Changed

```json
{
  "event": "queue-text-channel-changed",
  "data": {
    "textChannel": {
      "id": "12345",
      "name": "general"
    }
  }
}
```

### Member Joined / Removed / Updated

```json
{
  "event": "member-added", // member-added | member-removed | member-updated
  "data": {
    "id": "294448191808602112",
    "displayName": "Owl",
    "nickname": null,
    "username": "Owl",
    "discriminator": "9652",
    "avatar": "https://cdn.discordapp.com/avatars/294448191808602112/1065d499bca0e0272fe60d397f8c6c95.webp"
  }
}
```

### Member Jammed

```json
{
  "event": "member-jammed",
  "data": {
    "jams": [
      {
        "xOffset": 0.4319319053124271,
        "jamSpeed": 0.8230737904742744,
        "ySpeed": 0.9344855933992213
      }
    ],
    "member": {
      "id": "294448191808602112",
      "displayName": "Owl",
      "nickname": null,
      "username": "Owl",
      "discriminator": "9652",
      "avatar": "https://cdn.discordapp.com/avatars/294448191808602112/1065d499bca0e0272fe60d397f8c6c95.webp"
    }
  }
}
```

### Player Pause State Changed

```json
{
  "event": "player-pause-state-changed",
  "data": {
    "isPaused": true
  }
}
```

### Player Tick

```json
{
  "event": "player-tick",
  "data": {
    "position": 10000 // ms
  }
}
```

### Track Added / Removed / Skipped

```json
{
  "event": "track-added", // track-added | track-removed | track-skipped
  "data": {
    "track": {
      "id": "d5ceffe2-0c23-42ae-ab7b-305151637da3",
      "url": "https://youtu.be/_N6vSc_mT6I",
      "video": {
        "id": "_N6vSc_mT6I",
        "title": "TULUS - Hati-Hati di Jalan (Official Lyric Video)",
        "duration": 243,
        "thumbnails": [
          {
            "url": "https://i.ytimg.com/vi/_N6vSc_mT6I/hq720.jpg?sqp=-oaymwEjCOgCEMoBSFryq4qpAxUIARUAAAAAGAElAADIQj0AgKJDeAE=&rs=AOn4CLAGYEmBYZ98p0-W89nqc49HVqSrSg",
            "width": 360,
            "height": 202
          },
          {
            "url": "https://i.ytimg.com/vi/_N6vSc_mT6I/hq720.jpg?sqp=-oaymwEXCNAFEJQDSFryq4qpAwkIARUAAIhCGAE=&rs=AOn4CLBxA7gSFlYzGrkzskQZr2WGywyuig",
            "width": 720,
            "height": 404
          }
        ],
        "viewCount": "100450942",
        "channel": {
          "id": "UCRggxhdYIz0zSvUgJmCWMGg",
          "name": "Tulus",
          "thumbnails": [
            {
              "url": "https://yt3.ggpht.com/y4zoHuQG2_ZulwkfGZ0CCFNf9C-49XPB9eKDSepPNigzZ_1RRaWADFcY8OD1S6zNuXmWh2ypAA=s48-c-k-c0x00ffffff-no-nd-rj",
              "width": 48,
              "height": 48
            },
            {
              "url": "https://yt3.ggpht.com/y4zoHuQG2_ZulwkfGZ0CCFNf9C-49XPB9eKDSepPNigzZ_1RRaWADFcY8OD1S6zNuXmWh2ypAA=s88-c-k-c0x00ffffff-no-nd-rj",
              "width": 88,
              "height": 88
            },
            {
              "url": "https://yt3.ggpht.com/y4zoHuQG2_ZulwkfGZ0CCFNf9C-49XPB9eKDSepPNigzZ_1RRaWADFcY8OD1S6zNuXmWh2ypAA=s176-c-k-c0x00ffffff-no-nd-rj",
              "width": 176,
              "height": 176
            }
          ]
        }
      },
      "requestedBy": {
        "id": "294448191808602112",
        "displayName": "Owl",
        "nickname": null,
        "username": "Owl",
        "discriminator": "9652",
        "avatar": "https://cdn.discordapp.com/avatars/294448191808602112/1065d499bca0e0272fe60d397f8c6c95.webp"
      },
      "playedAt": null
    },
    "member": {
      "id": "294448191808602112",
      "displayName": "Owl",
      "nickname": null,
      "username": "Owl",
      "discriminator": "9652",
      "avatar": "https://cdn.discordapp.com/avatars/294448191808602112/1065d499bca0e0272fe60d397f8c6c95.webp"
    }
  }
}
```

### Track Order Changed

```json
{
  "event": "track-order-changed",
  "data": [
    "b9c099ab-443e-40cf-a55f-fde286979794",
    "4d9d2346-c852-4f8a-b606-46d2ede93f01",
    "941ae1c2-6f48-4ef5-b7a8-a6fb5b4cf9fa"
  ]
}
```

### Track Seeked

```json
{
  "event": "track-seeked",
  "data": {
    "position": 10000, // ms
    "member": {
      "id": "294448191808602112",
      "displayName": "Owl",
      "nickname": null,
      "username": "Owl",
      "discriminator": "9652",
      "avatar": "https://cdn.discordapp.com/avatars/294448191808602112/1065d499bca0e0272fe60d397f8c6c95.webp"
    }
  }
}
```

### Track Audio Started

```json
{
  "event": "track-audio-started",
  "data": {
    "id": "d5ceffe2-0c23-42ae-ab7b-305151637da3",
    "url": "https://youtu.be/_N6vSc_mT6I",
    "video": {
      "id": "_N6vSc_mT6I",
      "title": "TULUS - Hati-Hati di Jalan (Official Lyric Video)",
      "duration": 243,
      "thumbnails": [
        {
          "url": "https://i.ytimg.com/vi/_N6vSc_mT6I/hq720.jpg?sqp=-oaymwEjCOgCEMoBSFryq4qpAxUIARUAAAAAGAElAADIQj0AgKJDeAE=&rs=AOn4CLAGYEmBYZ98p0-W89nqc49HVqSrSg",
          "width": 360,
          "height": 202
        },
        {
          "url": "https://i.ytimg.com/vi/_N6vSc_mT6I/hq720.jpg?sqp=-oaymwEXCNAFEJQDSFryq4qpAwkIARUAAIhCGAE=&rs=AOn4CLBxA7gSFlYzGrkzskQZr2WGywyuig",
          "width": 720,
          "height": 404
        }
      ],
      "viewCount": "100450942",
      "channel": {
        "id": "UCRggxhdYIz0zSvUgJmCWMGg",
        "name": "Tulus",
        "thumbnails": [
          {
            "url": "https://yt3.ggpht.com/y4zoHuQG2_ZulwkfGZ0CCFNf9C-49XPB9eKDSepPNigzZ_1RRaWADFcY8OD1S6zNuXmWh2ypAA=s48-c-k-c0x00ffffff-no-nd-rj",
            "width": 48,
            "height": 48
          },
          {
            "url": "https://yt3.ggpht.com/y4zoHuQG2_ZulwkfGZ0CCFNf9C-49XPB9eKDSepPNigzZ_1RRaWADFcY8OD1S6zNuXmWh2ypAA=s88-c-k-c0x00ffffff-no-nd-rj",
            "width": 88,
            "height": 88
          },
          {
            "url": "https://yt3.ggpht.com/y4zoHuQG2_ZulwkfGZ0CCFNf9C-49XPB9eKDSepPNigzZ_1RRaWADFcY8OD1S6zNuXmWh2ypAA=s176-c-k-c0x00ffffff-no-nd-rj",
            "width": 176,
            "height": 176
          }
        ]
      }
    },
    "requestedBy": {
      "id": "294448191808602112",
      "displayName": "Owl",
      "nickname": null,
      "username": "Owl",
      "discriminator": "9652",
      "avatar": "https://cdn.discordapp.com/avatars/294448191808602112/1065d499bca0e0272fe60d397f8c6c95.webp"
    },
    "playedAt": null
  }
}
```

### Tracks Added / Removed

```json
{
  "event": "tracks-added",
  "data": {
    "tracks": [
      {
        "id": "d5ceffe2-0c23-42ae-ab7b-305151637da3",
        "url": "https://youtu.be/_N6vSc_mT6I",
        "video": {
          "id": "_N6vSc_mT6I",
          "title": "TULUS - Hati-Hati di Jalan (Official Lyric Video)",
          "duration": 243,
          "thumbnails": [
            {
              "url": "https://i.ytimg.com/vi/_N6vSc_mT6I/hq720.jpg?sqp=-oaymwEjCOgCEMoBSFryq4qpAxUIARUAAAAAGAElAADIQj0AgKJDeAE=&rs=AOn4CLAGYEmBYZ98p0-W89nqc49HVqSrSg",
              "width": 360,
              "height": 202
            },
            {
              "url": "https://i.ytimg.com/vi/_N6vSc_mT6I/hq720.jpg?sqp=-oaymwEXCNAFEJQDSFryq4qpAwkIARUAAIhCGAE=&rs=AOn4CLBxA7gSFlYzGrkzskQZr2WGywyuig",
              "width": 720,
              "height": 404
            }
          ],
          "viewCount": "100450942",
          "channel": {
            "id": "UCRggxhdYIz0zSvUgJmCWMGg",
            "name": "Tulus",
            "thumbnails": [
              {
                "url": "https://yt3.ggpht.com/y4zoHuQG2_ZulwkfGZ0CCFNf9C-49XPB9eKDSepPNigzZ_1RRaWADFcY8OD1S6zNuXmWh2ypAA=s48-c-k-c0x00ffffff-no-nd-rj",
                "width": 48,
                "height": 48
              },
              {
                "url": "https://yt3.ggpht.com/y4zoHuQG2_ZulwkfGZ0CCFNf9C-49XPB9eKDSepPNigzZ_1RRaWADFcY8OD1S6zNuXmWh2ypAA=s88-c-k-c0x00ffffff-no-nd-rj",
                "width": 88,
                "height": 88
              },
              {
                "url": "https://yt3.ggpht.com/y4zoHuQG2_ZulwkfGZ0CCFNf9C-49XPB9eKDSepPNigzZ_1RRaWADFcY8OD1S6zNuXmWh2ypAA=s176-c-k-c0x00ffffff-no-nd-rj",
                "width": 176,
                "height": 176
              }
            ]
          }
        },
        "requestedBy": {
          "id": "294448191808602112",
          "displayName": "Owl",
          "nickname": null,
          "username": "Owl",
          "discriminator": "9652",
          "avatar": "https://cdn.discordapp.com/avatars/294448191808602112/1065d499bca0e0272fe60d397f8c6c95.webp"
        },
        "playedAt": null
      }
    ],
    "member": {
      "id": "294448191808602112",
      "displayName": "Owl",
      "nickname": null,
      "username": "Owl",
      "discriminator": "9652",
      "avatar": "https://cdn.discordapp.com/avatars/294448191808602112/1065d499bca0e0272fe60d397f8c6c95.webp"
    }
  }
}
```
