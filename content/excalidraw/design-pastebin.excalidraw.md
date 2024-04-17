---

excalidraw-plugin: parsed
tags: [excalidraw]

---
==⚠  Switch to EXCALIDRAW VIEW in the MORE OPTIONS menu of this document. ⚠==


# Text Elements
pastebin.com ^taMxy4OJ

G ^QuG769ls

o ^YsAbMFXR

o ^QprRkfZN

g ^1vncqTly

l ^FIKBMGDV

e ^GSSeYg0s

Application
server ^NYJoWWM1

{ ^JeCVhQPG

} ^0TXMSTGa

DocumentDB
Shard 2 ^xq9JfVIj

pastes ^mh7S00EP

key: primary id
paste_data: str
title: str
expiry?: datetime
password?: hashed password
salt?: str
 ^dQcbzDA2

How to create a hash?

- We want a hash that uses
  letters and numbers.
- This 26 + 26 + 10 = 62 unique chars.
- 6 chars gives us ~10B possibilities.
- Encode each incremented value in Base62
  with length 6.

Example: pastebin.com/paste?id=aKfe2v

How do we deal with concurrent requests?
We don't want two pastes to use the same
counter value.

- We can have a coordination service that
  hands out exclusive "leases" to certain
  number ranges.
- E.g. Server 1 can use [1,9999], Server 2 
  can use [10000, 19999]. ^5NSJbYte

Application
server ^j1mGzDL9

Load
Balancer ^58vZyunl

{ ^tBr4Gpm0

} ^EekkYhBO

Document DB
Shard 1 ^ndbbminG

Sharding:

1. We could shard by key.

- All pastes with id starting with "a"
  would be created sequentially, leading
  to unbalanced loads.

2. We could shard by paste origin IP address.

- We might have to split it down further if one
  region is particularly busy.

3. We could shard by consistent hashing.

- Would have less hot spots than first option. ^AMVCmQWA

{ ^6RTiMYDc

} ^MeqOgX0N

{ ^AAqeBH4F

} ^QQDQcnLV

replicated for
durability and high
r/w ratio. ^XCaQo445

Distributed
Coordination
Service ^C9IuEUNj

manage
range
counters ^peJF0T3A

manage db
health ^IShTcgJQ

Key ^J3vYSsTg

Key ^pRNFkKzs

Value ^m35ZUkP8

Value ^FHFe9uIa

Cache ^WijvAxx6

Very popular pastes
can be cached to
reduce database load. ^QO0RSRKg

%%
# Drawing
```json
{
	"type": "excalidraw",
	"version": 2,
	"source": "https://github.com/zsviczian/obsidian-excalidraw-plugin/releases/tag/2.0.25",
	"elements": [
		{
			"id": "hFIvUb7F2vV22V8Z8JNmU",
			"type": "rectangle",
			"x": -464.69904386461724,
			"y": 58.66306745180839,
			"width": 382.9519805335757,
			"height": 441.9220184901691,
			"angle": 0,
			"strokeColor": "#1e1e1e",
			"backgroundColor": "#e9ecef",
			"fillStyle": "solid",
			"strokeWidth": 1,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"seed": 348503663,
			"version": 396,
			"versionNonce": 1044324385,
			"isDeleted": false,
			"boundElements": null,
			"updated": 1711505432359,
			"link": null,
			"locked": false
		},
		{
			"type": "text",
			"version": 773,
			"versionNonce": 1839820207,
			"isDeleted": false,
			"id": "taMxy4OJ",
			"fillStyle": "solid",
			"strokeWidth": 1,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -559.2084427087303,
			"y": -42.889193232363965,
			"strokeColor": "#000000",
			"backgroundColor": "#ced4da",
			"width": 99.01568603515625,
			"height": 22.383067689279017,
			"seed": 436643169,
			"groupIds": [
				"pHenT-vE08oFFgS8BMkwK"
			],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1711505429098,
			"link": null,
			"locked": false,
			"fontSize": 16.580050140206698,
			"fontFamily": 1,
			"text": "pastebin.com",
			"rawText": "pastebin.com",
			"textAlign": "center",
			"verticalAlign": "top",
			"containerId": null,
			"originalText": "pastebin.com",
			"lineHeight": 1.3499999999999985,
			"baseline": 14
		},
		{
			"type": "rectangle",
			"version": 2659,
			"versionNonce": 774949057,
			"isDeleted": false,
			"id": "Qlr3y2HXyzdelvvYyd8Hj",
			"fillStyle": "solid",
			"strokeWidth": 1,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -574.9215236411738,
			"y": -122.09006586316505,
			"strokeColor": "#000000",
			"backgroundColor": "#ffffff",
			"width": 130.441847900043,
			"height": 78.0679753427682,
			"seed": 1806520641,
			"groupIds": [
				"l144w_oj_qWzvcDwQTNGf",
				"pHenT-vE08oFFgS8BMkwK"
			],
			"frameId": null,
			"roundness": null,
			"boundElements": [
				{
					"id": "mV8aMpsQYSoIWgxwJpQ6a",
					"type": "arrow"
				}
			],
			"updated": 1711505429098,
			"link": null,
			"locked": false
		},
		{
			"type": "rectangle",
			"version": 1902,
			"versionNonce": 548265935,
			"isDeleted": false,
			"id": "ffRfleMWWHTU-fDBBHaLC",
			"fillStyle": "solid",
			"strokeWidth": 1,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -574.7399483479545,
			"y": -122.06785219234362,
			"strokeColor": "#000000",
			"backgroundColor": "#ced4da",
			"width": 129.58095857455965,
			"height": 12.717494608113203,
			"seed": 1330872609,
			"groupIds": [
				"l144w_oj_qWzvcDwQTNGf",
				"pHenT-vE08oFFgS8BMkwK"
			],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1711505429098,
			"link": null,
			"locked": false
		},
		{
			"type": "ellipse",
			"version": 2064,
			"versionNonce": 1903954081,
			"isDeleted": false,
			"id": "Bo5qdLq4RxzGSdfheOzvH",
			"fillStyle": "solid",
			"strokeWidth": 1,
			"strokeStyle": "solid",
			"roughness": 0,
			"opacity": 100,
			"angle": 0,
			"x": -570.3437156902318,
			"y": -118.61608238211139,
			"strokeColor": "#000000",
			"backgroundColor": "#fa5252",
			"width": 5.102005308169075,
			"height": 5.102005308169075,
			"seed": 1651029249,
			"groupIds": [
				"l144w_oj_qWzvcDwQTNGf",
				"pHenT-vE08oFFgS8BMkwK"
			],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1711505429098,
			"link": null,
			"locked": false
		},
		{
			"type": "ellipse",
			"version": 2108,
			"versionNonce": 2057244143,
			"isDeleted": false,
			"id": "4pSniiOOiHcvQr4A0zOyo",
			"fillStyle": "solid",
			"strokeWidth": 1,
			"strokeStyle": "solid",
			"roughness": 0,
			"opacity": 100,
			"angle": 0,
			"x": -559.8757395513034,
			"y": -118.61608238211139,
			"strokeColor": "#000000",
			"backgroundColor": "#fab005",
			"width": 5.102005308169075,
			"height": 5.102005308169075,
			"seed": 1751936225,
			"groupIds": [
				"l144w_oj_qWzvcDwQTNGf",
				"pHenT-vE08oFFgS8BMkwK"
			],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1711505429098,
			"link": null,
			"locked": false
		},
		{
			"type": "ellipse",
			"version": 2166,
			"versionNonce": 1293175937,
			"isDeleted": false,
			"id": "k-CGPl2kf9d3HnyERaTkM",
			"fillStyle": "solid",
			"strokeWidth": 1,
			"strokeStyle": "solid",
			"roughness": 0,
			"opacity": 100,
			"angle": 0,
			"x": -548.9480266531804,
			"y": -118.156345622901,
			"strokeColor": "#000000",
			"backgroundColor": "#40c057",
			"width": 5.102005308169075,
			"height": 5.102005308169075,
			"seed": 149825729,
			"groupIds": [
				"l144w_oj_qWzvcDwQTNGf",
				"pHenT-vE08oFFgS8BMkwK"
			],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1711505429098,
			"link": null,
			"locked": false
		},
		{
			"type": "text",
			"version": 425,
			"versionNonce": 718497697,
			"isDeleted": false,
			"id": "QuG769ls",
			"fillStyle": "hachure",
			"strokeWidth": 1,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -539.7696843769194,
			"y": -98.72964471077458,
			"strokeColor": "#228be6",
			"backgroundColor": "#ffffff",
			"width": 10.809295654296875,
			"height": 17.812824760471983,
			"seed": 1301112993,
			"groupIds": [
				"l144w_oj_qWzvcDwQTNGf",
				"pHenT-vE08oFFgS8BMkwK"
			],
			"frameId": null,
			"roundness": {
				"type": 2
			},
			"boundElements": [],
			"updated": 1711505704287,
			"link": null,
			"locked": false,
			"fontSize": 13.70217289267076,
			"fontFamily": 1,
			"text": "G",
			"rawText": "",
			"textAlign": "left",
			"verticalAlign": "top",
			"containerId": null,
			"originalText": "G",
			"lineHeight": 1.2999999999999996,
			"baseline": 12
		},
		{
			"type": "text",
			"version": 377,
			"versionNonce": 741416687,
			"isDeleted": false,
			"id": "YsAbMFXR",
			"fillStyle": "hachure",
			"strokeWidth": 1,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -526.7526201288816,
			"y": -98.72964471077458,
			"strokeColor": "#d9480f",
			"backgroundColor": "#ffffff",
			"width": 7.5897979736328125,
			"height": 17.812824760471983,
			"seed": 1610198145,
			"groupIds": [
				"l144w_oj_qWzvcDwQTNGf",
				"pHenT-vE08oFFgS8BMkwK"
			],
			"frameId": null,
			"roundness": {
				"type": 2
			},
			"boundElements": [],
			"updated": 1711505704288,
			"link": null,
			"locked": false,
			"fontSize": 13.702172892670754,
			"fontFamily": 1,
			"text": "o",
			"rawText": "",
			"textAlign": "left",
			"verticalAlign": "top",
			"containerId": null,
			"originalText": "o",
			"lineHeight": 1.3000000000000003,
			"baseline": 12
		},
		{
			"type": "text",
			"version": 384,
			"versionNonce": 1109904257,
			"isDeleted": false,
			"id": "QprRkfZN",
			"fillStyle": "hachure",
			"strokeWidth": 1,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -516.4759904593785,
			"y": -98.72964471077458,
			"strokeColor": "#fab005",
			"backgroundColor": "#ffffff",
			"width": 7.5897979736328125,
			"height": 17.812824760471983,
			"seed": 133330017,
			"groupIds": [
				"l144w_oj_qWzvcDwQTNGf",
				"pHenT-vE08oFFgS8BMkwK"
			],
			"frameId": null,
			"roundness": {
				"type": 2
			},
			"boundElements": [],
			"updated": 1711505704288,
			"link": null,
			"locked": false,
			"fontSize": 13.702172892670754,
			"fontFamily": 1,
			"text": "o",
			"rawText": "",
			"textAlign": "left",
			"verticalAlign": "top",
			"containerId": null,
			"originalText": "o",
			"lineHeight": 1.3000000000000003,
			"baseline": 12
		},
		{
			"type": "text",
			"version": 391,
			"versionNonce": 766339343,
			"isDeleted": false,
			"id": "1vncqTly",
			"fillStyle": "hachure",
			"strokeWidth": 1,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -506.88446943450947,
			"y": -98.72964471077458,
			"strokeColor": "#228be6",
			"backgroundColor": "#ffffff",
			"width": 6.8636932373046875,
			"height": 17.812824760471983,
			"seed": 1766277185,
			"groupIds": [
				"l144w_oj_qWzvcDwQTNGf",
				"pHenT-vE08oFFgS8BMkwK"
			],
			"frameId": null,
			"roundness": {
				"type": 2
			},
			"boundElements": [],
			"updated": 1711505704288,
			"link": null,
			"locked": false,
			"fontSize": 13.702172892670756,
			"fontFamily": 1,
			"text": "g",
			"rawText": "",
			"textAlign": "left",
			"verticalAlign": "top",
			"containerId": null,
			"originalText": "g",
			"lineHeight": 1.3,
			"baseline": 12
		},
		{
			"type": "text",
			"version": 393,
			"versionNonce": 1560589153,
			"isDeleted": false,
			"id": "FIKBMGDV",
			"fillStyle": "hachure",
			"strokeWidth": 1,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -498.66316569890716,
			"y": -98.72964471077458,
			"strokeColor": "#5c940d",
			"backgroundColor": "#ffffff",
			"width": 3.60308837890625,
			"height": 17.812824760471983,
			"seed": 30904353,
			"groupIds": [
				"l144w_oj_qWzvcDwQTNGf",
				"pHenT-vE08oFFgS8BMkwK"
			],
			"frameId": null,
			"roundness": {
				"type": 2
			},
			"boundElements": [],
			"updated": 1711505704288,
			"link": null,
			"locked": false,
			"fontSize": 13.702172892670756,
			"fontFamily": 1,
			"text": "l",
			"rawText": "",
			"textAlign": "left",
			"verticalAlign": "top",
			"containerId": null,
			"originalText": "l",
			"lineHeight": 1.3,
			"baseline": 12
		},
		{
			"type": "text",
			"version": 380,
			"versionNonce": 1767599919,
			"isDeleted": false,
			"id": "GSSeYg0s",
			"fillStyle": "hachure",
			"strokeWidth": 1,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -493.1822965418394,
			"y": -98.72964471077458,
			"strokeColor": "#d9480f",
			"backgroundColor": "#ffffff",
			"width": 7.493896484375,
			"height": 17.812824760471983,
			"seed": 1737679873,
			"groupIds": [
				"l144w_oj_qWzvcDwQTNGf",
				"pHenT-vE08oFFgS8BMkwK"
			],
			"frameId": null,
			"roundness": {
				"type": 2
			},
			"boundElements": [],
			"updated": 1711505704288,
			"link": null,
			"locked": false,
			"fontSize": 13.702172892670754,
			"fontFamily": 1,
			"text": "e",
			"rawText": "",
			"textAlign": "left",
			"verticalAlign": "top",
			"containerId": null,
			"originalText": "e",
			"lineHeight": 1.3000000000000003,
			"baseline": 12
		},
		{
			"type": "rectangle",
			"version": 313,
			"versionNonce": 878517871,
			"isDeleted": false,
			"id": "RtyGG-QPWqaJNUx7PTOSN",
			"fillStyle": "hachure",
			"strokeWidth": 1,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -552.8628718076926,
			"y": -77.24007022410288,
			"strokeColor": "#000000",
			"backgroundColor": "transparent",
			"width": 83.88774737623947,
			"height": 12.362404876498449,
			"seed": 1182317537,
			"groupIds": [
				"l144w_oj_qWzvcDwQTNGf",
				"pHenT-vE08oFFgS8BMkwK"
			],
			"frameId": null,
			"roundness": {
				"type": 1
			},
			"boundElements": [],
			"updated": 1711505429098,
			"link": null,
			"locked": false
		},
		{
			"type": "ellipse",
			"version": 349,
			"versionNonce": 576553985,
			"isDeleted": false,
			"id": "o2kUjAy468_Whg5msgizB",
			"fillStyle": "hachure",
			"strokeWidth": 1,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -479.12995700857823,
			"y": -74.14946900497844,
			"strokeColor": "#000000",
			"backgroundColor": "transparent",
			"width": 4.898891947531319,
			"height": 4.211328165421662,
			"seed": 513316801,
			"groupIds": [
				"VFRxpeEXDmIlIp7KulRte",
				"l144w_oj_qWzvcDwQTNGf",
				"pHenT-vE08oFFgS8BMkwK"
			],
			"frameId": null,
			"roundness": {
				"type": 2
			},
			"boundElements": [],
			"updated": 1711505429098,
			"link": null,
			"locked": false
		},
		{
			"type": "line",
			"version": 347,
			"versionNonce": 1596815503,
			"isDeleted": false,
			"id": "zTuWXC0YBEePtDZerw-mc",
			"fillStyle": "hachure",
			"strokeWidth": 1,
			"strokeStyle": "solid",
			"roughness": 2,
			"opacity": 100,
			"angle": 0,
			"x": -474.33759874132124,
			"y": -69.97560803999605,
			"strokeColor": "#000000",
			"backgroundColor": "transparent",
			"width": 2.492418710147513,
			"height": 3.1799824922571727,
			"seed": 1108473761,
			"groupIds": [
				"VFRxpeEXDmIlIp7KulRte",
				"l144w_oj_qWzvcDwQTNGf",
				"pHenT-vE08oFFgS8BMkwK"
			],
			"frameId": null,
			"roundness": {
				"type": 2
			},
			"boundElements": [],
			"updated": 1711505429098,
			"link": null,
			"locked": false,
			"startBinding": null,
			"endBinding": null,
			"lastCommittedPoint": null,
			"startArrowhead": null,
			"endArrowhead": null,
			"points": [
				[
					0,
					0
				],
				[
					2.492418710147513,
					3.1799824922571727
				]
			]
		},
		{
			"type": "rectangle",
			"version": 1318,
			"versionNonce": 250567649,
			"isDeleted": false,
			"id": "-g9U229-uuT580ENo3Isf",
			"fillStyle": "solid",
			"strokeWidth": 1,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -158.6043704085862,
			"y": -126.49924438885975,
			"strokeColor": "#000000",
			"backgroundColor": "#eeeeee",
			"width": 96.04882870779743,
			"height": 94.20173584803199,
			"seed": 1452589103,
			"groupIds": [
				"MStxC0Tdp7gnAvMqHsWM5"
			],
			"frameId": null,
			"roundness": null,
			"boundElements": [
				{
					"id": "Nvl6vknxrPx9OxSW4ZLWO",
					"type": "arrow"
				},
				{
					"id": "YxPmt5DjGUQwW2BBvhRWl",
					"type": "arrow"
				},
				{
					"id": "JLcBC_Je1UCxJ5-PfPWqi",
					"type": "arrow"
				}
			],
			"updated": 1711505429098,
			"link": null,
			"locked": false
		},
		{
			"type": "text",
			"version": 723,
			"versionNonce": 2142871361,
			"isDeleted": false,
			"id": "NYJoWWM1",
			"fillStyle": "solid",
			"strokeWidth": 1,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -148.48355102539068,
			"y": -99.48210933091488,
			"strokeColor": "#000000",
			"backgroundColor": "#ced4da",
			"width": 75.80718994140625,
			"height": 40.167465732141956,
			"seed": 629858895,
			"groupIds": [
				"MStxC0Tdp7gnAvMqHsWM5"
			],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1711505704288,
			"link": null,
			"locked": false,
			"fontSize": 14.876839160052583,
			"fontFamily": 1,
			"text": "Application\nserver",
			"rawText": "",
			"textAlign": "center",
			"verticalAlign": "top",
			"containerId": null,
			"originalText": "Application\nserver",
			"lineHeight": 1.3499999999999994,
			"baseline": 33
		},
		{
			"type": "rectangle",
			"version": 1317,
			"versionNonce": 1597716417,
			"isDeleted": false,
			"id": "_Ctghe3Vio8d5qrkqE_2e",
			"fillStyle": "solid",
			"strokeWidth": 1,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -148.6043704085862,
			"y": -116.49924438885975,
			"strokeColor": "#000000",
			"backgroundColor": "#eeeeee",
			"width": 96.04882870779743,
			"height": 94.20173584803199,
			"seed": 1514412239,
			"groupIds": [
				"u4QIkbVBaeqwpm0pZALVA"
			],
			"frameId": null,
			"roundness": null,
			"boundElements": [
				{
					"id": "Nvl6vknxrPx9OxSW4ZLWO",
					"type": "arrow"
				},
				{
					"id": "mMK6u1slZDB417Rym_362",
					"type": "arrow"
				}
			],
			"updated": 1711505429098,
			"link": null,
			"locked": false
		},
		{
			"type": "text",
			"version": 723,
			"versionNonce": 698593615,
			"isDeleted": false,
			"id": "j1mGzDL9",
			"fillStyle": "solid",
			"strokeWidth": 1,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -138.48355102539068,
			"y": -89.48210933091488,
			"strokeColor": "#000000",
			"backgroundColor": "#ced4da",
			"width": 75.80718994140625,
			"height": 40.167465732141956,
			"seed": 1849810849,
			"groupIds": [
				"u4QIkbVBaeqwpm0pZALVA"
			],
			"frameId": null,
			"roundness": null,
			"boundElements": null,
			"updated": 1711505704288,
			"link": null,
			"locked": false,
			"fontSize": 14.876839160052583,
			"fontFamily": 1,
			"text": "Application\nserver",
			"rawText": "",
			"textAlign": "center",
			"verticalAlign": "top",
			"containerId": null,
			"originalText": "Application\nserver",
			"lineHeight": 1.3499999999999994,
			"baseline": 33
		},
		{
			"id": "mV8aMpsQYSoIWgxwJpQ6a",
			"type": "arrow",
			"x": -437.495388051748,
			"y": -81.84176635742188,
			"width": 89.44983406595657,
			"height": 0,
			"angle": 0,
			"strokeColor": "#1e1e1e",
			"backgroundColor": "transparent",
			"fillStyle": "solid",
			"strokeWidth": 1,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"groupIds": [],
			"frameId": null,
			"roundness": {
				"type": 2
			},
			"seed": 854558255,
			"version": 268,
			"versionNonce": 358651809,
			"isDeleted": false,
			"boundElements": null,
			"updated": 1711505429098,
			"link": null,
			"locked": false,
			"points": [
				[
					0,
					0
				],
				[
					89.44983406595657,
					0
				]
			],
			"lastCommittedPoint": [
				117.7603759765625,
				0
			],
			"startBinding": {
				"elementId": "Qlr3y2HXyzdelvvYyd8Hj",
				"focus": 0.031109089970054352,
				"gap": 6.984287689382796
			},
			"endBinding": {
				"elementId": "IaJpcnLwyFlm5sHdokl4q",
				"focus": -0.02505325248836985,
				"gap": 10.367258995973259
			},
			"startArrowhead": null,
			"endArrowhead": "arrow"
		},
		{
			"type": "line",
			"version": 5765,
			"versionNonce": 1615785711,
			"isDeleted": false,
			"id": "916DaUDQaflZh2n1H6zWQ",
			"fillStyle": "solid",
			"strokeWidth": 1,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": 112.7210162330939,
			"y": -133.90116437733678,
			"strokeColor": "#000000",
			"backgroundColor": "#ced4da",
			"width": 76.99810389727404,
			"height": 99.3782771160576,
			"seed": 1860303567,
			"groupIds": [
				"m5xcy2F7qggAj6DhR3gG0",
				"kAfAcTxj3UjAp-yCh1_hN",
				"45DRwR2SmlWEBd4v1ulyR"
			],
			"frameId": null,
			"roundness": {
				"type": 2
			},
			"boundElements": null,
			"updated": 1711505429098,
			"link": null,
			"locked": false,
			"startBinding": null,
			"endBinding": null,
			"lastCommittedPoint": null,
			"startArrowhead": null,
			"endArrowhead": null,
			"points": [
				[
					0,
					0
				],
				[
					0.25390020469272123,
					75.10956320658954
				],
				[
					0.011881933539366223,
					83.66046081728857
				],
				[
					3.9655726433067375,
					87.35519793732486
				],
				[
					17.73410326369428,
					90.48214189738947
				],
				[
					41.00682018880676,
					91.45582553513545
				],
				[
					63.24236222825349,
					89.90119697892054
				],
				[
					75.05626943052894,
					86.18333090428511
				],
				[
					76.72246117951802,
					83.04913080160064
				],
				[
					76.95647177899504,
					76.16486549140681
				],
				[
					76.77280066894052,
					6.301273122914302
				],
				[
					76.35874703071867,
					-0.299549116207539
				],
				[
					71.41469198102895,
					-3.9887920872726523
				],
				[
					61.003567150978974,
					-6.125406402086429
				],
				[
					37.27802033642641,
					-7.922451580922154
				],
				[
					18.256149021768273,
					-6.850869494392455
				],
				[
					3.2955764171578545,
					-3.2161938062295934
				],
				[
					-0.04163211827899763,
					-0.0451306156134037
				],
				[
					0,
					0
				]
			]
		},
		{
			"type": "ellipse",
			"version": 6523,
			"versionNonce": 1133443969,
			"isDeleted": false,
			"id": "CTzRpFpWVMQ2jd99NLTmP",
			"fillStyle": "solid",
			"strokeWidth": 1,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": 112.22734849115398,
			"y": -142.67209100097097,
			"strokeColor": "#000000",
			"backgroundColor": "#fff",
			"width": 76.50422544892463,
			"height": 15.472404032124233,
			"seed": 1100466415,
			"groupIds": [
				"m5xcy2F7qggAj6DhR3gG0",
				"kAfAcTxj3UjAp-yCh1_hN",
				"45DRwR2SmlWEBd4v1ulyR"
			],
			"frameId": null,
			"roundness": null,
			"boundElements": [
				{
					"id": "xSFadLZ2kYxm8htj9ZmjS",
					"type": "arrow"
				}
			],
			"updated": 1711505429098,
			"link": null,
			"locked": false
		},
		{
			"type": "text",
			"version": 1725,
			"versionNonce": 2024148769,
			"isDeleted": false,
			"id": "tBr4Gpm0",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": 131.2299268527928,
			"y": -107.98513482611969,
			"strokeColor": "#495057",
			"backgroundColor": "transparent",
			"width": 17.115234375,
			"height": 36,
			"seed": 1957614351,
			"groupIds": [
				"kAfAcTxj3UjAp-yCh1_hN",
				"45DRwR2SmlWEBd4v1ulyR"
			],
			"frameId": null,
			"roundness": {
				"type": 2
			},
			"boundElements": null,
			"updated": 1711505704289,
			"link": null,
			"locked": false,
			"fontSize": 29.219434366479078,
			"fontFamily": 3,
			"text": "{",
			"rawText": "",
			"textAlign": "left",
			"verticalAlign": "top",
			"containerId": null,
			"originalText": "{",
			"lineHeight": 1.2320567040578883,
			"baseline": 28
		},
		{
			"type": "text",
			"version": 1699,
			"versionNonce": 1474211695,
			"isDeleted": false,
			"id": "EekkYhBO",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": 153.2408001985383,
			"y": -107.50842485420065,
			"strokeColor": "#495057",
			"backgroundColor": "transparent",
			"width": 17.21484375,
			"height": 35.94436319458793,
			"seed": 1621072175,
			"groupIds": [
				"kAfAcTxj3UjAp-yCh1_hN",
				"45DRwR2SmlWEBd4v1ulyR"
			],
			"frameId": null,
			"roundness": {
				"type": 2
			},
			"boundElements": null,
			"updated": 1711505704289,
			"link": null,
			"locked": false,
			"fontSize": 29.384515916572173,
			"fontFamily": 3,
			"text": "}",
			"rawText": "",
			"textAlign": "left",
			"verticalAlign": "top",
			"containerId": null,
			"originalText": "}",
			"lineHeight": 1.2232416316348487,
			"baseline": 28
		},
		{
			"type": "text",
			"version": 917,
			"versionNonce": 1816477487,
			"isDeleted": false,
			"id": "ndbbminG",
			"fillStyle": "solid",
			"strokeWidth": 1,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": 90.80776977539062,
			"y": -41.88307933839376,
			"strokeColor": "#000000",
			"backgroundColor": "transparent",
			"width": 120.27362060546875,
			"height": 51.732382114989065,
			"seed": 986880847,
			"groupIds": [
				"45DRwR2SmlWEBd4v1ulyR"
			],
			"frameId": null,
			"roundness": null,
			"boundElements": [
				{
					"id": "CzoMex3ErycdVWThqPyq9",
					"type": "arrow"
				}
			],
			"updated": 1711505429098,
			"link": null,
			"locked": false,
			"fontSize": 18.16360832146819,
			"fontFamily": 1,
			"text": "Document DB\nShard 1",
			"rawText": "Document DB\nShard 1",
			"textAlign": "center",
			"verticalAlign": "top",
			"containerId": null,
			"originalText": "Document DB\nShard 1",
			"lineHeight": 1.4240667712990924,
			"baseline": 43
		},
		{
			"id": "Nvl6vknxrPx9OxSW4ZLWO",
			"type": "arrow",
			"x": -40.041443053332046,
			"y": -80.78054809570312,
			"width": 141.52424258336134,
			"height": 0,
			"angle": 0,
			"strokeColor": "#1e1e1e",
			"backgroundColor": "transparent",
			"fillStyle": "solid",
			"strokeWidth": 1,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"groupIds": [],
			"frameId": null,
			"roundness": {
				"type": 2
			},
			"seed": 1703227233,
			"version": 182,
			"versionNonce": 1427427137,
			"isDeleted": false,
			"boundElements": null,
			"updated": 1711505429098,
			"link": null,
			"locked": false,
			"points": [
				[
					0,
					0
				],
				[
					141.52424258336134,
					0
				]
			],
			"lastCommittedPoint": [
				151.727783203125,
				0
			],
			"startBinding": {
				"elementId": "_Ctghe3Vio8d5qrkqE_2e",
				"focus": -0.24165524187837276,
				"gap": 12.514098647456713
			},
			"endBinding": null,
			"startArrowhead": null,
			"endArrowhead": "arrow"
		},
		{
			"type": "rectangle",
			"version": 442,
			"versionNonce": 1322484047,
			"isDeleted": false,
			"id": "tYTlC7T3ZbhuAdIiGrNdS",
			"fillStyle": "hachure",
			"strokeWidth": 1,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": 190.84066567350374,
			"y": -360.851443917437,
			"strokeColor": "#000000",
			"backgroundColor": "transparent",
			"width": 270.12152099609375,
			"height": 177.50888652522457,
			"seed": 1422701281,
			"groupIds": [
				"73Phh9lh08KUAQZ3qEEwV"
			],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1711505429098,
			"link": null,
			"locked": false
		},
		{
			"type": "line",
			"version": 320,
			"versionNonce": 1528512289,
			"isDeleted": false,
			"id": "i8Wu4Plv6-5S6hFlss_XM",
			"fillStyle": "hachure",
			"strokeWidth": 1,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": 193.26601967741,
			"y": -322.2948338100151,
			"strokeColor": "#000000",
			"backgroundColor": "transparent",
			"width": 269.38385009765625,
			"height": 1.72381591796875,
			"seed": 1297460929,
			"groupIds": [
				"73Phh9lh08KUAQZ3qEEwV"
			],
			"frameId": null,
			"roundness": {
				"type": 2
			},
			"boundElements": [],
			"updated": 1711505429098,
			"link": null,
			"locked": false,
			"startBinding": null,
			"endBinding": null,
			"lastCommittedPoint": null,
			"startArrowhead": null,
			"endArrowhead": null,
			"points": [
				[
					0,
					0
				],
				[
					269.38385009765625,
					-1.72381591796875
				]
			]
		},
		{
			"id": "mh7S00EP",
			"type": "text",
			"x": 199.2352404674889,
			"y": -353.97718181776617,
			"width": 67.15992736816406,
			"height": 25,
			"angle": 0,
			"strokeColor": "#1e1e1e",
			"backgroundColor": "transparent",
			"fillStyle": "solid",
			"strokeWidth": 1,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"groupIds": [
				"73Phh9lh08KUAQZ3qEEwV"
			],
			"frameId": null,
			"roundness": null,
			"seed": 2049929633,
			"version": 224,
			"versionNonce": 1721007983,
			"isDeleted": false,
			"boundElements": null,
			"updated": 1711505429098,
			"link": null,
			"locked": false,
			"text": "pastes",
			"rawText": "pastes",
			"fontSize": 20,
			"fontFamily": 1,
			"textAlign": "left",
			"verticalAlign": "top",
			"baseline": 16,
			"containerId": null,
			"originalText": "pastes",
			"lineHeight": 1.25
		},
		{
			"id": "dQcbzDA2",
			"type": "text",
			"x": 200.76200955417153,
			"y": -313.21813241366556,
			"width": 221.4077911376953,
			"height": 140,
			"angle": 0,
			"strokeColor": "#1e1e1e",
			"backgroundColor": "transparent",
			"fillStyle": "solid",
			"strokeWidth": 1,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"groupIds": [
				"73Phh9lh08KUAQZ3qEEwV"
			],
			"frameId": null,
			"roundness": null,
			"seed": 1681367727,
			"version": 301,
			"versionNonce": 1518908161,
			"isDeleted": false,
			"boundElements": null,
			"updated": 1711505429098,
			"link": null,
			"locked": false,
			"text": "key: primary id\npaste_data: str\ntitle: str\nexpiry?: datetime\npassword?: hashed password\nsalt?: str\n",
			"rawText": "key: primary id\npaste_data: str\ntitle: str\nexpiry?: datetime\npassword?: hashed password\nsalt?: str\n",
			"fontSize": 16,
			"fontFamily": 1,
			"textAlign": "left",
			"verticalAlign": "top",
			"baseline": 134,
			"containerId": null,
			"originalText": "key: primary id\npaste_data: str\ntitle: str\nexpiry?: datetime\npassword?: hashed password\nsalt?: str\n",
			"lineHeight": 1.25
		},
		{
			"id": "5NSJbYte",
			"type": "text",
			"x": -446.05215113775375,
			"y": 79.94456321624887,
			"width": 350.0958251953125,
			"height": 400,
			"angle": 0,
			"strokeColor": "#1e1e1e",
			"backgroundColor": "transparent",
			"fillStyle": "solid",
			"strokeWidth": 1,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"seed": 450916207,
			"version": 1242,
			"versionNonce": 1351119873,
			"isDeleted": false,
			"boundElements": null,
			"updated": 1711505432359,
			"link": null,
			"locked": false,
			"text": "How to create a hash?\n\n- We want a hash that uses\n  letters and numbers.\n- This 26 + 26 + 10 = 62 unique chars.\n- 6 chars gives us ~10B possibilities.\n- Encode each incremented value in Base62\n  with length 6.\n\nExample: pastebin.com/paste?id=aKfe2v\n\nHow do we deal with concurrent requests?\nWe don't want two pastes to use the same\ncounter value.\n\n- We can have a coordination service that\n  hands out exclusive \"leases\" to certain\n  number ranges.\n- E.g. Server 1 can use [1,9999], Server 2 \n  can use [10000, 19999].",
			"rawText": "How to create a hash?\n\n- We want a hash that uses\n  letters and numbers.\n- This 26 + 26 + 10 = 62 unique chars.\n- 6 chars gives us ~10B possibilities.\n- Encode each incremented value in Base62\n  with length 6.\n\nExample: pastebin.com/paste?id=aKfe2v\n\nHow do we deal with concurrent requests?\nWe don't want two pastes to use the same\ncounter value.\n\n- We can have a coordination service that\n  hands out exclusive \"leases\" to certain\n  number ranges.\n- E.g. Server 1 can use [1,9999], Server 2 \n  can use [10000, 19999].",
			"fontSize": 16,
			"fontFamily": 1,
			"textAlign": "left",
			"verticalAlign": "top",
			"baseline": 394,
			"containerId": null,
			"originalText": "How to create a hash?\n\n- We want a hash that uses\n  letters and numbers.\n- This 26 + 26 + 10 = 62 unique chars.\n- 6 chars gives us ~10B possibilities.\n- Encode each incremented value in Base62\n  with length 6.\n\nExample: pastebin.com/paste?id=aKfe2v\n\nHow do we deal with concurrent requests?\nWe don't want two pastes to use the same\ncounter value.\n\n- We can have a coordination service that\n  hands out exclusive \"leases\" to certain\n  number ranges.\n- E.g. Server 1 can use [1,9999], Server 2 \n  can use [10000, 19999].",
			"lineHeight": 1.25
		},
		{
			"type": "rectangle",
			"version": 1872,
			"versionNonce": 400337633,
			"isDeleted": false,
			"id": "IaJpcnLwyFlm5sHdokl4q",
			"fillStyle": "solid",
			"strokeWidth": 1,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 90,
			"angle": 0,
			"x": -337.6782949898182,
			"y": -185.2656833880012,
			"strokeColor": "#000000",
			"backgroundColor": "#eeeeee",
			"width": 69.69390497296568,
			"height": 201.7922810927382,
			"seed": 1493382927,
			"groupIds": [
				"EKaKmKFzZwGMixP8DQIcy",
				"tgQXC2o7wn6n6voSRS0Ke"
			],
			"frameId": null,
			"roundness": null,
			"boundElements": [
				{
					"id": "mV8aMpsQYSoIWgxwJpQ6a",
					"type": "arrow"
				},
				{
					"id": "YxPmt5DjGUQwW2BBvhRWl",
					"type": "arrow"
				}
			],
			"updated": 1711505429098,
			"link": null,
			"locked": false
		},
		{
			"type": "ellipse",
			"version": 1688,
			"versionNonce": 1640017839,
			"isDeleted": false,
			"id": "2SKtz1p_0XgSqj0F8h4Nc",
			"fillStyle": "solid",
			"strokeWidth": 1,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -294.5465493972002,
			"y": -115.38123237553538,
			"strokeColor": "#000000",
			"backgroundColor": "#868e96",
			"width": 18.463181339628875,
			"height": 17.895083452255665,
			"seed": 80182575,
			"groupIds": [
				"U_D8VpnGrZgav5SPXnV_v",
				"EKaKmKFzZwGMixP8DQIcy",
				"tgQXC2o7wn6n6voSRS0Ke"
			],
			"frameId": null,
			"roundness": {
				"type": 2
			},
			"boundElements": [
				{
					"type": "arrow",
					"id": "o97vzsyvTja_SH5JBGbLG"
				},
				{
					"type": "arrow",
					"id": "cDbW6WmRHxNB9dDp1Ep_p"
				}
			],
			"updated": 1711505429098,
			"link": null,
			"locked": false
		},
		{
			"type": "ellipse",
			"version": 1997,
			"versionNonce": 463906497,
			"isDeleted": false,
			"id": "e_CXcohzLCpdVKfSikmLH",
			"fillStyle": "solid",
			"strokeWidth": 1,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -330.61030831078557,
			"y": -118.2731675506862,
			"strokeColor": "#000000",
			"backgroundColor": "#868e96",
			"width": 18.463181339628875,
			"height": 17.895083452255665,
			"seed": 1482555215,
			"groupIds": [
				"U_D8VpnGrZgav5SPXnV_v",
				"EKaKmKFzZwGMixP8DQIcy",
				"tgQXC2o7wn6n6voSRS0Ke"
			],
			"frameId": null,
			"roundness": {
				"type": 2
			},
			"boundElements": [
				{
					"type": "arrow",
					"id": "E-nmj2Q8KwAt0l6_OywS9"
				},
				{
					"type": "arrow",
					"id": "o97vzsyvTja_SH5JBGbLG"
				},
				{
					"type": "arrow",
					"id": "cDbW6WmRHxNB9dDp1Ep_p"
				}
			],
			"updated": 1711505429098,
			"link": null,
			"locked": false
		},
		{
			"type": "ellipse",
			"version": 1995,
			"versionNonce": 1418518991,
			"isDeleted": false,
			"id": "F7j7oPm3KVYzxy_Q4Wx2A",
			"fillStyle": "solid",
			"strokeWidth": 1,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -294.05479390042916,
			"y": -64.78159077875853,
			"strokeColor": "#000000",
			"backgroundColor": "#868e96",
			"width": 18.463181339628875,
			"height": 17.895083452255665,
			"seed": 371146095,
			"groupIds": [
				"U_D8VpnGrZgav5SPXnV_v",
				"EKaKmKFzZwGMixP8DQIcy",
				"tgQXC2o7wn6n6voSRS0Ke"
			],
			"frameId": null,
			"roundness": {
				"type": 2
			},
			"boundElements": [
				{
					"type": "arrow",
					"id": "cDbW6WmRHxNB9dDp1Ep_p"
				}
			],
			"updated": 1711505429098,
			"link": null,
			"locked": false
		},
		{
			"type": "ellipse",
			"version": 1712,
			"versionNonce": 814098081,
			"isDeleted": false,
			"id": "wEW6ARwCn5mo7g39Vrrvx",
			"fillStyle": "solid",
			"strokeWidth": 1,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -294.73651136526456,
			"y": -166.96617298269905,
			"strokeColor": "#000000",
			"backgroundColor": "#868e96",
			"width": 18.463181339628875,
			"height": 17.895083452255665,
			"seed": 559134607,
			"groupIds": [
				"U_D8VpnGrZgav5SPXnV_v",
				"EKaKmKFzZwGMixP8DQIcy",
				"tgQXC2o7wn6n6voSRS0Ke"
			],
			"frameId": null,
			"roundness": {
				"type": 2
			},
			"boundElements": [
				{
					"type": "arrow",
					"id": "o97vzsyvTja_SH5JBGbLG"
				}
			],
			"updated": 1711505429098,
			"link": null,
			"locked": false
		},
		{
			"type": "arrow",
			"version": 5715,
			"versionNonce": 525193199,
			"isDeleted": false,
			"id": "E-nmj2Q8KwAt0l6_OywS9",
			"fillStyle": "solid",
			"strokeWidth": 1,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -317.54117606657275,
			"y": -100.0580796306379,
			"strokeColor": "#000000",
			"backgroundColor": "transparent",
			"width": 26.68308902555831,
			"height": 37.58197677119037,
			"seed": 1614015919,
			"groupIds": [
				"U_D8VpnGrZgav5SPXnV_v",
				"EKaKmKFzZwGMixP8DQIcy",
				"tgQXC2o7wn6n6voSRS0Ke"
			],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1711505429099,
			"link": null,
			"locked": false,
			"startBinding": {
				"elementId": "e_CXcohzLCpdVKfSikmLH",
				"focus": 0.2447201201770933,
				"gap": 1.042956544145886
			},
			"endBinding": null,
			"lastCommittedPoint": null,
			"startArrowhead": null,
			"endArrowhead": "arrow",
			"points": [
				[
					0,
					0
				],
				[
					26.68308902555831,
					37.58197677119037
				]
			]
		},
		{
			"type": "arrow",
			"version": 4336,
			"versionNonce": 556444289,
			"isDeleted": false,
			"id": "cDbW6WmRHxNB9dDp1Ep_p",
			"fillStyle": "solid",
			"strokeWidth": 1,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -311.55588418093936,
			"y": -109.0501453396385,
			"strokeColor": "#000000",
			"backgroundColor": "transparent",
			"width": 16.61130383973117,
			"height": 1.3207328297184937,
			"seed": 1575509967,
			"groupIds": [
				"U_D8VpnGrZgav5SPXnV_v",
				"EKaKmKFzZwGMixP8DQIcy",
				"tgQXC2o7wn6n6voSRS0Ke"
			],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1711505429099,
			"link": null,
			"locked": false,
			"startBinding": {
				"elementId": "e_CXcohzLCpdVKfSikmLH",
				"focus": -0.056308402661334404,
				"gap": 1
			},
			"endBinding": {
				"elementId": "2SKtz1p_0XgSqj0F8h4Nc",
				"focus": 0.05904577717458803,
				"gap": 1
			},
			"lastCommittedPoint": null,
			"startArrowhead": null,
			"endArrowhead": "arrow",
			"points": [
				[
					0,
					0
				],
				[
					16.61130383973117,
					1.3207328297184937
				]
			]
		},
		{
			"type": "arrow",
			"version": 5293,
			"versionNonce": 1544288783,
			"isDeleted": false,
			"id": "o97vzsyvTja_SH5JBGbLG",
			"fillStyle": "solid",
			"strokeWidth": 1,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -316.01938100600324,
			"y": -117.50425173902414,
			"strokeColor": "#000000",
			"backgroundColor": "transparent",
			"width": 25.400417044718434,
			"height": 32.52973567190321,
			"seed": 747212271,
			"groupIds": [
				"U_D8VpnGrZgav5SPXnV_v",
				"EKaKmKFzZwGMixP8DQIcy",
				"tgQXC2o7wn6n6voSRS0Ke"
			],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1711505429099,
			"link": null,
			"locked": false,
			"startBinding": {
				"elementId": "e_CXcohzLCpdVKfSikmLH",
				"focus": -0.08869372840676859,
				"gap": 1
			},
			"endBinding": {
				"elementId": "wEW6ARwCn5mo7g39Vrrvx",
				"focus": -0.09679793421697702,
				"gap": 1
			},
			"lastCommittedPoint": null,
			"startArrowhead": null,
			"endArrowhead": "arrow",
			"points": [
				[
					0,
					0
				],
				[
					25.400417044718434,
					-32.52973567190321
				]
			]
		},
		{
			"type": "text",
			"version": 768,
			"versionNonce": 507085569,
			"isDeleted": false,
			"id": "58vZyunl",
			"fillStyle": "solid",
			"strokeWidth": 1,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -334.3225610702298,
			"y": -28.873280062687627,
			"strokeColor": "#000000",
			"backgroundColor": "transparent",
			"width": 62.98243713378906,
			"height": 40,
			"seed": 119535631,
			"groupIds": [
				"tgQXC2o7wn6n6voSRS0Ke"
			],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1711505704290,
			"link": null,
			"locked": false,
			"fontSize": 14.751291676011752,
			"fontFamily": 1,
			"text": "Load\nBalancer",
			"rawText": "",
			"textAlign": "center",
			"verticalAlign": "top",
			"containerId": null,
			"originalText": "Load\nBalancer",
			"lineHeight": 1.355813473102399,
			"baseline": 33
		},
		{
			"id": "YxPmt5DjGUQwW2BBvhRWl",
			"type": "arrow",
			"x": -258.2414703111234,
			"y": -81.49868045712742,
			"width": 85.1638756985642,
			"height": 0,
			"angle": 0,
			"strokeColor": "#1e1e1e",
			"backgroundColor": "transparent",
			"fillStyle": "solid",
			"strokeWidth": 1,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"groupIds": [],
			"frameId": null,
			"roundness": {
				"type": 2
			},
			"seed": 2033772065,
			"version": 50,
			"versionNonce": 1337974831,
			"isDeleted": false,
			"boundElements": null,
			"updated": 1711505429099,
			"link": null,
			"locked": false,
			"points": [
				[
					0,
					0
				],
				[
					85.1638756985642,
					0
				]
			],
			"lastCommittedPoint": [
				85.1638756985642,
				0
			],
			"startBinding": {
				"elementId": "IaJpcnLwyFlm5sHdokl4q",
				"focus": 0.028453639246838396,
				"gap": 9.742919705729093
			},
			"endBinding": {
				"elementId": "-g9U229-uuT580ENo3Isf",
				"focus": 0.04459161974832227,
				"gap": 14.473224203973025
			},
			"startArrowhead": null,
			"endArrowhead": "arrow"
		},
		{
			"type": "line",
			"version": 5842,
			"versionNonce": 1959837249,
			"isDeleted": false,
			"id": "jHAbbDQWKJDwHRGnVYtD_",
			"fillStyle": "solid",
			"strokeWidth": 1,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": 261.9171450953222,
			"y": -133.90116437733678,
			"strokeColor": "#000000",
			"backgroundColor": "#ced4da",
			"width": 76.99810389727404,
			"height": 99.37827711605759,
			"seed": 681496527,
			"groupIds": [
				"HEKQdvnVmmc3-rj6OG6f9",
				"ZPXLrP1YyvYwPJGdt-rsM",
				"i3fjObCVpm4d84hlx_DhD"
			],
			"frameId": null,
			"roundness": {
				"type": 2
			},
			"boundElements": [],
			"updated": 1711505429099,
			"link": null,
			"locked": false,
			"startBinding": null,
			"endBinding": null,
			"lastCommittedPoint": null,
			"startArrowhead": null,
			"endArrowhead": null,
			"points": [
				[
					0,
					0
				],
				[
					0.25390020469272123,
					75.10956320658954
				],
				[
					0.011881933539366223,
					83.66046081728857
				],
				[
					3.9655726433067375,
					87.35519793732486
				],
				[
					17.73410326369428,
					90.48214189738947
				],
				[
					41.00682018880676,
					91.45582553513545
				],
				[
					63.24236222825349,
					89.90119697892054
				],
				[
					75.05626943052894,
					86.18333090428511
				],
				[
					76.72246117951802,
					83.04913080160064
				],
				[
					76.95647177899504,
					76.16486549140681
				],
				[
					76.77280066894052,
					6.301273122914302
				],
				[
					76.35874703071867,
					-0.299549116207539
				],
				[
					71.41469198102895,
					-3.9887920872726523
				],
				[
					61.003567150978974,
					-6.125406402086429
				],
				[
					37.27802033642641,
					-7.922451580922154
				],
				[
					18.256149021768273,
					-6.850869494392455
				],
				[
					3.2955764171578545,
					-3.2161938062295934
				],
				[
					-0.04163211827899763,
					-0.0451306156134037
				],
				[
					0,
					0
				]
			]
		},
		{
			"type": "ellipse",
			"version": 6600,
			"versionNonce": 206701135,
			"isDeleted": false,
			"id": "4PJrgoU99WaXONvVvJ6Ap",
			"fillStyle": "solid",
			"strokeWidth": 1,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": 261.4234773533823,
			"y": -142.67209100097097,
			"strokeColor": "#000000",
			"backgroundColor": "#fff",
			"width": 76.50422544892463,
			"height": 15.472404032124233,
			"seed": 921828847,
			"groupIds": [
				"HEKQdvnVmmc3-rj6OG6f9",
				"ZPXLrP1YyvYwPJGdt-rsM",
				"i3fjObCVpm4d84hlx_DhD"
			],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1711505429099,
			"link": null,
			"locked": false
		},
		{
			"type": "text",
			"version": 1803,
			"versionNonce": 508881295,
			"isDeleted": false,
			"id": "JeCVhQPG",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": 280.4260557150211,
			"y": -107.98513482611969,
			"strokeColor": "#495057",
			"backgroundColor": "transparent",
			"width": 17.115234375,
			"height": 36,
			"seed": 184182799,
			"groupIds": [
				"ZPXLrP1YyvYwPJGdt-rsM",
				"i3fjObCVpm4d84hlx_DhD"
			],
			"frameId": null,
			"roundness": {
				"type": 2
			},
			"boundElements": [],
			"updated": 1711505704290,
			"link": null,
			"locked": false,
			"fontSize": 29.219434366479078,
			"fontFamily": 3,
			"text": "{",
			"rawText": "",
			"textAlign": "left",
			"verticalAlign": "top",
			"containerId": null,
			"originalText": "{",
			"lineHeight": 1.2320567040578883,
			"baseline": 28
		},
		{
			"type": "text",
			"version": 1777,
			"versionNonce": 1291025121,
			"isDeleted": false,
			"id": "0TXMSTGa",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": 302.4369290607666,
			"y": -107.50842485420065,
			"strokeColor": "#495057",
			"backgroundColor": "transparent",
			"width": 17.21484375,
			"height": 35.94436319458793,
			"seed": 850431535,
			"groupIds": [
				"ZPXLrP1YyvYwPJGdt-rsM",
				"i3fjObCVpm4d84hlx_DhD"
			],
			"frameId": null,
			"roundness": {
				"type": 2
			},
			"boundElements": [],
			"updated": 1711505704290,
			"link": null,
			"locked": false,
			"fontSize": 29.384515916572173,
			"fontFamily": 3,
			"text": "}",
			"rawText": "",
			"textAlign": "left",
			"verticalAlign": "top",
			"containerId": null,
			"originalText": "}",
			"lineHeight": 1.2232416316348487,
			"baseline": 28
		},
		{
			"type": "text",
			"version": 1017,
			"versionNonce": 1632952833,
			"isDeleted": false,
			"id": "xq9JfVIj",
			"fillStyle": "solid",
			"strokeWidth": 1,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": 244.54389192375174,
			"y": -41.88307933839376,
			"strokeColor": "#000000",
			"backgroundColor": "transparent",
			"width": 111.19363403320312,
			"height": 51.732382114989065,
			"seed": 1761407055,
			"groupIds": [
				"i3fjObCVpm4d84hlx_DhD"
			],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1711505429099,
			"link": null,
			"locked": false,
			"fontSize": 18.16360832146819,
			"fontFamily": 1,
			"text": "DocumentDB\nShard 2",
			"rawText": "DocumentDB\nShard 2",
			"textAlign": "center",
			"verticalAlign": "top",
			"containerId": null,
			"originalText": "DocumentDB\nShard 2",
			"lineHeight": 1.4240667712990924,
			"baseline": 43
		},
		{
			"id": "31NNBLY8d7j_KxbSfyRoA",
			"type": "rectangle",
			"x": 184.20059657858747,
			"y": 48.60344052501091,
			"width": 415.58371628123905,
			"height": 345.86952874970723,
			"angle": 0,
			"strokeColor": "#1e1e1e",
			"backgroundColor": "#e9ecef",
			"fillStyle": "solid",
			"strokeWidth": 1,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"groupIds": [
				"KIyZiiGlI3Fhc9vBkfBZu"
			],
			"frameId": null,
			"roundness": null,
			"seed": 2092510561,
			"version": 490,
			"versionNonce": 646527969,
			"isDeleted": false,
			"boundElements": null,
			"updated": 1711505435561,
			"link": null,
			"locked": false
		},
		{
			"id": "AMVCmQWA",
			"type": "text",
			"x": 208.46205488631017,
			"y": 59.3933592817757,
			"width": 373.19976806640625,
			"height": 320,
			"angle": 0,
			"strokeColor": "#1e1e1e",
			"backgroundColor": "transparent",
			"fillStyle": "solid",
			"strokeWidth": 1,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"groupIds": [
				"KIyZiiGlI3Fhc9vBkfBZu"
			],
			"frameId": null,
			"roundness": null,
			"seed": 1490467887,
			"version": 952,
			"versionNonce": 681121729,
			"isDeleted": false,
			"boundElements": null,
			"updated": 1711505435561,
			"link": null,
			"locked": false,
			"text": "Sharding:\n\n1. We could shard by key.\n\n- All pastes with id starting with \"a\"\n  would be created sequentially, leading\n  to unbalanced loads.\n\n2. We could shard by paste origin IP address.\n\n- We might have to split it down further if one\n  region is particularly busy.\n\n3. We could shard by consistent hashing.\n\n- Would have less hot spots than first option.",
			"rawText": "Sharding:\n\n1. We could shard by key.\n\n- All pastes with id starting with \"a\"\n  would be created sequentially, leading\n  to unbalanced loads.\n\n2. We could shard by paste origin IP address.\n\n- We might have to split it down further if one\n  region is particularly busy.\n\n3. We could shard by consistent hashing.\n\n- Would have less hot spots than first option.",
			"fontSize": 16,
			"fontFamily": 1,
			"textAlign": "left",
			"verticalAlign": "top",
			"baseline": 314,
			"containerId": null,
			"originalText": "Sharding:\n\n1. We could shard by key.\n\n- All pastes with id starting with \"a\"\n  would be created sequentially, leading\n  to unbalanced loads.\n\n2. We could shard by paste origin IP address.\n\n- We might have to split it down further if one\n  region is particularly busy.\n\n3. We could shard by consistent hashing.\n\n- Would have less hot spots than first option.",
			"lineHeight": 1.25
		},
		{
			"type": "line",
			"version": 5882,
			"versionNonce": 1986187439,
			"isDeleted": false,
			"id": "i02l0fczbFLXT56Ps53ox",
			"fillStyle": "solid",
			"strokeWidth": 1,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": 126.10051063267309,
			"y": -146.7395418594704,
			"strokeColor": "#000000",
			"backgroundColor": "#ced4da",
			"width": 76.99810389727404,
			"height": 99.3782771160576,
			"seed": 1331958337,
			"groupIds": [
				"axAmub6qPoocqoTDjKAHz",
				"Vqxvy8riNkbaPyz1WJsAo",
				"l2yIBUTtN5QkaOZFhkEJi"
			],
			"frameId": null,
			"roundness": {
				"type": 2
			},
			"boundElements": [],
			"updated": 1711505429099,
			"link": null,
			"locked": false,
			"startBinding": null,
			"endBinding": null,
			"lastCommittedPoint": null,
			"startArrowhead": null,
			"endArrowhead": null,
			"points": [
				[
					0,
					0
				],
				[
					0.25390020469272123,
					75.10956320658954
				],
				[
					0.011881933539366223,
					83.66046081728857
				],
				[
					3.9655726433067375,
					87.35519793732486
				],
				[
					17.73410326369428,
					90.48214189738947
				],
				[
					41.00682018880676,
					91.45582553513545
				],
				[
					63.24236222825349,
					89.90119697892054
				],
				[
					75.05626943052894,
					86.18333090428511
				],
				[
					76.72246117951802,
					83.04913080160064
				],
				[
					76.95647177899504,
					76.16486549140681
				],
				[
					76.77280066894052,
					6.301273122914302
				],
				[
					76.35874703071867,
					-0.299549116207539
				],
				[
					71.41469198102895,
					-3.9887920872726523
				],
				[
					61.003567150978974,
					-6.125406402086429
				],
				[
					37.27802033642641,
					-7.922451580922154
				],
				[
					18.256149021768273,
					-6.850869494392455
				],
				[
					3.2955764171578545,
					-3.2161938062295934
				],
				[
					-0.04163211827899763,
					-0.0451306156134037
				],
				[
					0,
					0
				]
			]
		},
		{
			"type": "ellipse",
			"version": 6640,
			"versionNonce": 846403009,
			"isDeleted": false,
			"id": "zNSUTvhT5z_J9tSyjiz2I",
			"fillStyle": "solid",
			"strokeWidth": 1,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": 125.60684289073316,
			"y": -155.51046848310457,
			"strokeColor": "#000000",
			"backgroundColor": "#fff",
			"width": 76.50422544892463,
			"height": 15.472404032124233,
			"seed": 1888100897,
			"groupIds": [
				"axAmub6qPoocqoTDjKAHz",
				"Vqxvy8riNkbaPyz1WJsAo",
				"l2yIBUTtN5QkaOZFhkEJi"
			],
			"frameId": null,
			"roundness": null,
			"boundElements": [
				{
					"id": "xSFadLZ2kYxm8htj9ZmjS",
					"type": "arrow"
				}
			],
			"updated": 1711505429099,
			"link": null,
			"locked": false
		},
		{
			"type": "text",
			"version": 1842,
			"versionNonce": 1245634479,
			"isDeleted": false,
			"id": "6RTiMYDc",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": 144.609421252372,
			"y": -120.8235123082533,
			"strokeColor": "#495057",
			"backgroundColor": "transparent",
			"width": 17.115234375,
			"height": 36,
			"seed": 1176712705,
			"groupIds": [
				"Vqxvy8riNkbaPyz1WJsAo",
				"l2yIBUTtN5QkaOZFhkEJi"
			],
			"frameId": null,
			"roundness": {
				"type": 2
			},
			"boundElements": [],
			"updated": 1711505704291,
			"link": null,
			"locked": false,
			"fontSize": 29.219434366479078,
			"fontFamily": 3,
			"text": "{",
			"rawText": "",
			"textAlign": "left",
			"verticalAlign": "top",
			"containerId": null,
			"originalText": "{",
			"lineHeight": 1.2320567040578883,
			"baseline": 28
		},
		{
			"type": "text",
			"version": 1816,
			"versionNonce": 627275457,
			"isDeleted": false,
			"id": "MeqOgX0N",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": 166.62029459811748,
			"y": -120.34680233633426,
			"strokeColor": "#495057",
			"backgroundColor": "transparent",
			"width": 17.21484375,
			"height": 35.94436319458793,
			"seed": 1395576289,
			"groupIds": [
				"Vqxvy8riNkbaPyz1WJsAo",
				"l2yIBUTtN5QkaOZFhkEJi"
			],
			"frameId": null,
			"roundness": {
				"type": 2
			},
			"boundElements": [],
			"updated": 1711505704291,
			"link": null,
			"locked": false,
			"fontSize": 29.384515916572173,
			"fontFamily": 3,
			"text": "}",
			"rawText": "",
			"textAlign": "left",
			"verticalAlign": "top",
			"containerId": null,
			"originalText": "}",
			"lineHeight": 1.2232416316348487,
			"baseline": 28
		},
		{
			"type": "line",
			"version": 5809,
			"versionNonce": 949727471,
			"isDeleted": false,
			"id": "ZupShIl-HW8fpz29OMXZC",
			"fillStyle": "solid",
			"strokeWidth": 1,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": 273.9626933956397,
			"y": -144.55967756701878,
			"strokeColor": "#000000",
			"backgroundColor": "#ced4da",
			"width": 76.99810389727404,
			"height": 99.3782771160576,
			"seed": 505654095,
			"groupIds": [
				"WSpOuRoUZeEvpZjIMuUQj",
				"RfsXW3CGkcWf6b7MH7nE7",
				"_4hgVuWr2KRZZb1GRA5ly"
			],
			"frameId": null,
			"roundness": {
				"type": 2
			},
			"boundElements": [],
			"updated": 1711505429099,
			"link": null,
			"locked": false,
			"startBinding": null,
			"endBinding": null,
			"lastCommittedPoint": null,
			"startArrowhead": null,
			"endArrowhead": null,
			"points": [
				[
					0,
					0
				],
				[
					0.25390020469272123,
					75.10956320658954
				],
				[
					0.011881933539366223,
					83.66046081728857
				],
				[
					3.9655726433067375,
					87.35519793732486
				],
				[
					17.73410326369428,
					90.48214189738947
				],
				[
					41.00682018880676,
					91.45582553513545
				],
				[
					63.24236222825349,
					89.90119697892054
				],
				[
					75.05626943052894,
					86.18333090428511
				],
				[
					76.72246117951802,
					83.04913080160064
				],
				[
					76.95647177899504,
					76.16486549140681
				],
				[
					76.77280066894052,
					6.301273122914302
				],
				[
					76.35874703071867,
					-0.299549116207539
				],
				[
					71.41469198102895,
					-3.9887920872726523
				],
				[
					61.003567150978974,
					-6.125406402086429
				],
				[
					37.27802033642641,
					-7.922451580922154
				],
				[
					18.256149021768273,
					-6.850869494392455
				],
				[
					3.2955764171578545,
					-3.2161938062295934
				],
				[
					-0.04163211827899763,
					-0.0451306156134037
				],
				[
					0,
					0
				]
			]
		},
		{
			"type": "ellipse",
			"version": 6566,
			"versionNonce": 1961318785,
			"isDeleted": false,
			"id": "u-6cnA2GEWT9CNpK700hF",
			"fillStyle": "solid",
			"strokeWidth": 1,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": 273.46902565369976,
			"y": -153.33060419065296,
			"strokeColor": "#000000",
			"backgroundColor": "#fff",
			"width": 76.50422544892463,
			"height": 15.472404032124233,
			"seed": 1850698095,
			"groupIds": [
				"WSpOuRoUZeEvpZjIMuUQj",
				"RfsXW3CGkcWf6b7MH7nE7",
				"_4hgVuWr2KRZZb1GRA5ly"
			],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1711505429099,
			"link": null,
			"locked": false
		},
		{
			"type": "text",
			"version": 1768,
			"versionNonce": 854965007,
			"isDeleted": false,
			"id": "AAqeBH4F",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": 292.4716040153386,
			"y": -118.64364801580169,
			"strokeColor": "#495057",
			"backgroundColor": "transparent",
			"width": 17.115234375,
			"height": 36,
			"seed": 1520329615,
			"groupIds": [
				"RfsXW3CGkcWf6b7MH7nE7",
				"_4hgVuWr2KRZZb1GRA5ly"
			],
			"frameId": null,
			"roundness": {
				"type": 2
			},
			"boundElements": [],
			"updated": 1711505429099,
			"link": null,
			"locked": false,
			"fontSize": 29.219434366479078,
			"fontFamily": 3,
			"text": "{",
			"rawText": "{",
			"textAlign": "left",
			"verticalAlign": "top",
			"containerId": null,
			"originalText": "{",
			"lineHeight": 1.2320567040578883,
			"baseline": 28
		},
		{
			"type": "text",
			"version": 1742,
			"versionNonce": 1822589281,
			"isDeleted": false,
			"id": "QQDQcnLV",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": 314.4824773610841,
			"y": -118.16693804388265,
			"strokeColor": "#495057",
			"backgroundColor": "transparent",
			"width": 17.21484375,
			"height": 35.94436319458793,
			"seed": 1934170543,
			"groupIds": [
				"RfsXW3CGkcWf6b7MH7nE7",
				"_4hgVuWr2KRZZb1GRA5ly"
			],
			"frameId": null,
			"roundness": {
				"type": 2
			},
			"boundElements": [],
			"updated": 1711505429099,
			"link": null,
			"locked": false,
			"fontSize": 29.384515916572173,
			"fontFamily": 3,
			"text": "}",
			"rawText": "}",
			"textAlign": "left",
			"verticalAlign": "top",
			"containerId": null,
			"originalText": "}",
			"lineHeight": 1.2232416316348487,
			"baseline": 28
		},
		{
			"id": "tt9iAmLev9WDItSmlNCIP",
			"type": "arrow",
			"x": 412.97655578080503,
			"y": -101.80758480003293,
			"width": 53.464642976781306,
			"height": 9.813717516154398,
			"angle": 0,
			"strokeColor": "#1e1e1e",
			"backgroundColor": "#e9ecef",
			"fillStyle": "solid",
			"strokeWidth": 1,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"seed": 2053129409,
			"version": 266,
			"versionNonce": 97091887,
			"isDeleted": false,
			"boundElements": null,
			"updated": 1711505429099,
			"link": null,
			"locked": false,
			"points": [
				[
					0,
					0
				],
				[
					-53.464642976781306,
					-9.813717516154398
				]
			],
			"lastCommittedPoint": [
				-106.43155335055167,
				0
			],
			"startBinding": {
				"elementId": "XCaQo445",
				"focus": -0.028207906694177616,
				"gap": 10.371717328669092
			},
			"endBinding": null,
			"startArrowhead": null,
			"endArrowhead": "arrow"
		},
		{
			"id": "XCaQo445",
			"type": "text",
			"x": 423.3482731094741,
			"y": -118.06668862325569,
			"width": 142.20790100097656,
			"height": 60,
			"angle": 0,
			"strokeColor": "#1e1e1e",
			"backgroundColor": "#e9ecef",
			"fillStyle": "solid",
			"strokeWidth": 1,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"seed": 262968609,
			"version": 297,
			"versionNonce": 913157441,
			"isDeleted": false,
			"boundElements": [
				{
					"id": "tt9iAmLev9WDItSmlNCIP",
					"type": "arrow"
				}
			],
			"updated": 1711505429099,
			"link": null,
			"locked": false,
			"text": "replicated for\ndurability and high\nr/w ratio.",
			"rawText": "replicated for\ndurability and high\nr/w ratio.",
			"fontSize": 16,
			"fontFamily": 1,
			"textAlign": "left",
			"verticalAlign": "top",
			"baseline": 54,
			"containerId": null,
			"originalText": "replicated for\ndurability and high\nr/w ratio.",
			"lineHeight": 1.25
		},
		{
			"id": "FbjSbOnDi9_jjDLj_UdAV",
			"type": "rectangle",
			"x": -95.84683323230422,
			"y": -404.2837465753579,
			"width": 112.43651956259738,
			"height": 98.87415616102251,
			"angle": 0,
			"strokeColor": "#1e1e1e",
			"backgroundColor": "#e9ecef",
			"fillStyle": "solid",
			"strokeWidth": 1,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"seed": 1918523393,
			"version": 213,
			"versionNonce": 1920959311,
			"isDeleted": false,
			"boundElements": [
				{
					"type": "text",
					"id": "C9IuEUNj"
				},
				{
					"id": "JLcBC_Je1UCxJ5-PfPWqi",
					"type": "arrow"
				},
				{
					"id": "xSFadLZ2kYxm8htj9ZmjS",
					"type": "arrow"
				}
			],
			"updated": 1711505429099,
			"link": null,
			"locked": false
		},
		{
			"id": "C9IuEUNj",
			"type": "text",
			"x": -86.90054610725554,
			"y": -384.84666849484665,
			"width": 94.5439453125,
			"height": 60,
			"angle": 0,
			"strokeColor": "#1e1e1e",
			"backgroundColor": "#e9ecef",
			"fillStyle": "solid",
			"strokeWidth": 1,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"seed": 245882977,
			"version": 225,
			"versionNonce": 430464289,
			"isDeleted": false,
			"boundElements": null,
			"updated": 1711505429099,
			"link": null,
			"locked": false,
			"text": "Distributed\nCoordination\nService",
			"rawText": "Distributed\nCoordination\nService",
			"fontSize": 16,
			"fontFamily": 1,
			"textAlign": "center",
			"verticalAlign": "middle",
			"baseline": 54,
			"containerId": "FbjSbOnDi9_jjDLj_UdAV",
			"originalText": "Distributed\nCoordination\nService",
			"lineHeight": 1.25
		},
		{
			"id": "JLcBC_Je1UCxJ5-PfPWqi",
			"type": "arrow",
			"x": -100.83852007753998,
			"y": -144.06653694884585,
			"width": 27.642255966693895,
			"height": 149.05046728598478,
			"angle": 0,
			"strokeColor": "#1e1e1e",
			"backgroundColor": "#e9ecef",
			"fillStyle": "solid",
			"strokeWidth": 1,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"seed": 1159829583,
			"version": 169,
			"versionNonce": 2037399919,
			"isDeleted": false,
			"boundElements": [
				{
					"type": "text",
					"id": "peJF0T3A"
				}
			],
			"updated": 1711505429099,
			"link": null,
			"locked": false,
			"points": [
				[
					0,
					0
				],
				[
					27.642255966693895,
					-149.05046728598478
				]
			],
			"lastCommittedPoint": [
				47.77328981817078,
				-106.162149228955
			],
			"startBinding": {
				"elementId": "-g9U229-uuT580ENo3Isf",
				"gap": 17.567292559986107,
				"focus": -0.0394438117095896
			},
			"endBinding": {
				"elementId": "FbjSbOnDi9_jjDLj_UdAV",
				"gap": 12.29258617950478,
				"focus": 0.33828885259789765
			},
			"startArrowhead": null,
			"endArrowhead": "arrow"
		},
		{
			"id": "peJF0T3A",
			"type": "text",
			"x": -128.31024008353089,
			"y": -225.49972851752833,
			"width": 66.81596374511719,
			"height": 60,
			"angle": 0,
			"strokeColor": "#1e1e1e",
			"backgroundColor": "#e9ecef",
			"fillStyle": "solid",
			"strokeWidth": 1,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"seed": 321227983,
			"version": 29,
			"versionNonce": 1170346241,
			"isDeleted": false,
			"boundElements": null,
			"updated": 1711505429099,
			"link": null,
			"locked": false,
			"text": "manage\nrange\ncounters",
			"rawText": "manage\nrange\ncounters",
			"fontSize": 16,
			"fontFamily": 1,
			"textAlign": "center",
			"verticalAlign": "middle",
			"baseline": 54,
			"containerId": "JLcBC_Je1UCxJ5-PfPWqi",
			"originalText": "manage\nrange\ncounters",
			"lineHeight": 1.25
		},
		{
			"id": "xSFadLZ2kYxm8htj9ZmjS",
			"type": "arrow",
			"x": -1.618320982775657,
			"y": -291.2327980270038,
			"width": 144.9429872974866,
			"height": 125.95219834435426,
			"angle": 0,
			"strokeColor": "#1e1e1e",
			"backgroundColor": "#e9ecef",
			"fillStyle": "solid",
			"strokeWidth": 1,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"seed": 813846447,
			"version": 212,
			"versionNonce": 2078555023,
			"isDeleted": false,
			"boundElements": [
				{
					"type": "text",
					"id": "IShTcgJQ"
				}
			],
			"updated": 1711505429099,
			"link": null,
			"locked": false,
			"points": [
				[
					0,
					0
				],
				[
					144.9429872974866,
					125.95219834435426
				]
			],
			"lastCommittedPoint": [
				105.3642603713879,
				105.26650807381418
			],
			"startBinding": {
				"elementId": "FbjSbOnDi9_jjDLj_UdAV",
				"gap": 14.176792387331602,
				"focus": 0.31116061087017777
			},
			"endBinding": {
				"elementId": "zNSUTvhT5z_J9tSyjiz2I",
				"gap": 11.484732970457515,
				"focus": -0.009889144503090027
			},
			"startArrowhead": null,
			"endArrowhead": "arrow"
		},
		{
			"id": "IShTcgJQ",
			"type": "text",
			"x": 30.08191509083599,
			"y": -248.5167667449943,
			"width": 80.94395446777344,
			"height": 40,
			"angle": 0,
			"strokeColor": "#1e1e1e",
			"backgroundColor": "#e9ecef",
			"fillStyle": "solid",
			"strokeWidth": 1,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"seed": 1729371329,
			"version": 37,
			"versionNonce": 1345997025,
			"isDeleted": false,
			"boundElements": null,
			"updated": 1711505429099,
			"link": null,
			"locked": false,
			"text": "manage db\nhealth",
			"rawText": "manage db\nhealth",
			"fontSize": 16,
			"fontFamily": 1,
			"textAlign": "center",
			"verticalAlign": "middle",
			"baseline": 34,
			"containerId": "xSFadLZ2kYxm8htj9ZmjS",
			"originalText": "manage db\nhealth",
			"lineHeight": 1.25
		},
		{
			"type": "rectangle",
			"version": 1854,
			"versionNonce": 504623535,
			"isDeleted": false,
			"id": "FB58yCOt_UJaZ_TkmPGoT",
			"fillStyle": "solid",
			"strokeWidth": 1,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -17.739443493244778,
			"y": 53.759443586444746,
			"strokeColor": "#000000",
			"backgroundColor": "#eeeeee",
			"width": 120.49648094110887,
			"height": 88.23967962722799,
			"seed": 555749903,
			"groupIds": [
				"Slu1BuXYmob_hgWlngIMh",
				"PF2HmJersAWA4aRaBQ8N6"
			],
			"frameId": null,
			"roundness": {
				"type": 1
			},
			"boundElements": [
				{
					"id": "mMK6u1slZDB417Rym_362",
					"type": "arrow"
				},
				{
					"id": "CzoMex3ErycdVWThqPyq9",
					"type": "arrow"
				}
			],
			"updated": 1711505429099,
			"link": null,
			"locked": false
		},
		{
			"type": "rectangle",
			"version": 1519,
			"versionNonce": 1923122369,
			"isDeleted": false,
			"id": "BGyzjAyCgX4aUomXlW_9a",
			"fillStyle": "solid",
			"strokeWidth": 1,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -10.008474583304121,
			"y": 60.6906570919065,
			"strokeColor": "#000000",
			"backgroundColor": "#868e96",
			"width": 25.05900267359336,
			"height": 9.863649988542074,
			"seed": 177272879,
			"groupIds": [
				"sDoK5lwp-qn1e13n3CuJz",
				"Slu1BuXYmob_hgWlngIMh",
				"PF2HmJersAWA4aRaBQ8N6"
			],
			"frameId": null,
			"roundness": null,
			"boundElements": [
				{
					"type": "arrow",
					"id": "FJLtWDtDULzWS8M-4aDH5"
				}
			],
			"updated": 1711505429099,
			"link": null,
			"locked": false
		},
		{
			"type": "rectangle",
			"version": 1860,
			"versionNonce": 1764221903,
			"isDeleted": false,
			"id": "kNIC5cWYsYDGocPRDfdpl",
			"fillStyle": "solid",
			"strokeWidth": 1,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": 29.8726615865815,
			"y": 60.281127764645504,
			"strokeColor": "#000000",
			"backgroundColor": "#ced4da",
			"width": 66.11311343671451,
			"height": 10.663405393018481,
			"seed": 2101353039,
			"groupIds": [
				"sDoK5lwp-qn1e13n3CuJz",
				"Slu1BuXYmob_hgWlngIMh",
				"PF2HmJersAWA4aRaBQ8N6"
			],
			"frameId": null,
			"roundness": {
				"type": 1
			},
			"boundElements": [
				{
					"type": "arrow",
					"id": "FJLtWDtDULzWS8M-4aDH5"
				}
			],
			"updated": 1711505429099,
			"link": null,
			"locked": false
		},
		{
			"type": "arrow",
			"version": 7386,
			"versionNonce": 143934625,
			"isDeleted": false,
			"id": "FJLtWDtDULzWS8M-4aDH5",
			"fillStyle": "solid",
			"strokeWidth": 1,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": 16.611519633081173,
			"y": 66.03176620629259,
			"strokeColor": "#000000",
			"backgroundColor": "#ced4da",
			"width": 14.110644515372014,
			"height": 0.1286692574004148,
			"seed": 772143215,
			"groupIds": [
				"sDoK5lwp-qn1e13n3CuJz",
				"Slu1BuXYmob_hgWlngIMh",
				"PF2HmJersAWA4aRaBQ8N6"
			],
			"frameId": null,
			"roundness": {
				"type": 2
			},
			"boundElements": [],
			"updated": 1711505429099,
			"link": null,
			"locked": false,
			"startBinding": {
				"elementId": "J3vYSsTg",
				"focus": 0.03340258771226859,
				"gap": 9.092720869612144
			},
			"endBinding": {
				"elementId": "KqL4RAxgPsmFgG9zbRhL9",
				"focus": 2.456132592376025,
				"gap": 8.206444049758318
			},
			"lastCommittedPoint": null,
			"startArrowhead": null,
			"endArrowhead": "arrow",
			"points": [
				[
					0,
					0
				],
				[
					14.110644515372014,
					-0.1286692574004148
				]
			]
		},
		{
			"type": "rectangle",
			"version": 1592,
			"versionNonce": 758682095,
			"isDeleted": false,
			"id": "zgHd55j70_OFpoJH3Z1Vw",
			"fillStyle": "solid",
			"strokeWidth": 1,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -9.581938367582495,
			"y": 73.91327977924962,
			"strokeColor": "#000000",
			"backgroundColor": "#868e96",
			"width": 25.05900267359336,
			"height": 9.863649988542074,
			"seed": 581636751,
			"groupIds": [
				"d8uU7broE3m3qnQRob4GS",
				"Slu1BuXYmob_hgWlngIMh",
				"PF2HmJersAWA4aRaBQ8N6"
			],
			"frameId": null,
			"roundness": null,
			"boundElements": [
				{
					"type": "arrow",
					"id": "AadhtsCu7XY-ED6vixQMV"
				},
				{
					"type": "arrow",
					"id": "FJLtWDtDULzWS8M-4aDH5"
				}
			],
			"updated": 1711505429099,
			"link": null,
			"locked": false
		},
		{
			"type": "rectangle",
			"version": 1944,
			"versionNonce": 1304758401,
			"isDeleted": false,
			"id": "KqL4RAxgPsmFgG9zbRhL9",
			"fillStyle": "solid",
			"strokeWidth": 1,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": 30.299197802300398,
			"y": 74.10954099865049,
			"strokeColor": "#000000",
			"backgroundColor": "#ced4da",
			"width": 66.11311343671451,
			"height": 10.663405393018481,
			"seed": 333965487,
			"groupIds": [
				"d8uU7broE3m3qnQRob4GS",
				"Slu1BuXYmob_hgWlngIMh",
				"PF2HmJersAWA4aRaBQ8N6"
			],
			"frameId": null,
			"roundness": {
				"type": 1
			},
			"boundElements": [
				{
					"type": "arrow",
					"id": "AadhtsCu7XY-ED6vixQMV"
				},
				{
					"type": "arrow",
					"id": "FJLtWDtDULzWS8M-4aDH5"
				}
			],
			"updated": 1711505429099,
			"link": null,
			"locked": false
		},
		{
			"type": "arrow",
			"version": 8137,
			"versionNonce": 592346127,
			"isDeleted": false,
			"id": "AadhtsCu7XY-ED6vixQMV",
			"fillStyle": "solid",
			"strokeWidth": 1,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": 16.31331799196579,
			"y": 79.528670590816,
			"strokeColor": "#000000",
			"backgroundColor": "#ced4da",
			"width": 14.105872619241076,
			"height": 0.026745107590664598,
			"seed": 258276047,
			"groupIds": [
				"d8uU7broE3m3qnQRob4GS",
				"Slu1BuXYmob_hgWlngIMh",
				"PF2HmJersAWA4aRaBQ8N6"
			],
			"frameId": null,
			"roundness": {
				"type": 2
			},
			"boundElements": [],
			"updated": 1711505429099,
			"link": null,
			"locked": false,
			"startBinding": {
				"elementId": "J3vYSsTg",
				"focus": 3.289050236557561,
				"gap": 9.417440996672298
			},
			"endBinding": {
				"elementId": "zgHd55j70_OFpoJH3Z1Vw",
				"focus": -0.13282478031960193,
				"gap": 14.942126305196004
			},
			"lastCommittedPoint": null,
			"startArrowhead": null,
			"endArrowhead": "arrow",
			"points": [
				[
					0,
					0
				],
				[
					14.105872619241076,
					0.026745107590664598
				]
			]
		},
		{
			"type": "rectangle",
			"version": 1730,
			"versionNonce": 1542606945,
			"isDeleted": false,
			"id": "2V0EbiB_FzbvF-L0tlTJb",
			"fillStyle": "solid",
			"strokeWidth": 1,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -8.995451070969864,
			"y": 101.56573170947209,
			"strokeColor": "#000000",
			"backgroundColor": "#868e96",
			"width": 25.05900267359336,
			"height": 9.863649988542074,
			"seed": 1505413359,
			"groupIds": [
				"InEB-GremyZ7WgGrtBcwg",
				"Slu1BuXYmob_hgWlngIMh",
				"PF2HmJersAWA4aRaBQ8N6"
			],
			"frameId": null,
			"roundness": null,
			"boundElements": [
				{
					"type": "arrow",
					"id": "vOHLflugLaWsyIDboF8jJ"
				}
			],
			"updated": 1711505429099,
			"link": null,
			"locked": false
		},
		{
			"type": "rectangle",
			"version": 2065,
			"versionNonce": 1331831343,
			"isDeleted": false,
			"id": "Ss2RI_KHlx9JToX9bSRy9",
			"fillStyle": "solid",
			"strokeWidth": 1,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": 30.88568509891826,
			"y": 101.45909765554157,
			"strokeColor": "#000000",
			"backgroundColor": "#ced4da",
			"width": 66.11311343671451,
			"height": 10.663405393018481,
			"seed": 275895055,
			"groupIds": [
				"InEB-GremyZ7WgGrtBcwg",
				"Slu1BuXYmob_hgWlngIMh",
				"PF2HmJersAWA4aRaBQ8N6"
			],
			"frameId": null,
			"roundness": {
				"type": 1
			},
			"boundElements": [
				{
					"type": "arrow",
					"id": "vOHLflugLaWsyIDboF8jJ"
				}
			],
			"updated": 1711505429099,
			"link": null,
			"locked": false
		},
		{
			"type": "arrow",
			"version": 9052,
			"versionNonce": 1760271425,
			"isDeleted": false,
			"id": "vOHLflugLaWsyIDboF8jJ",
			"fillStyle": "solid",
			"strokeWidth": 1,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": 17.144204308916926,
			"y": 107.19395002070829,
			"strokeColor": "#000000",
			"backgroundColor": "#ced4da",
			"width": 14.110644515372014,
			"height": 0.06608807192479067,
			"seed": 201496879,
			"groupIds": [
				"InEB-GremyZ7WgGrtBcwg",
				"Slu1BuXYmob_hgWlngIMh",
				"PF2HmJersAWA4aRaBQ8N6"
			],
			"frameId": null,
			"roundness": {
				"type": 2
			},
			"boundElements": [],
			"updated": 1711505429099,
			"link": null,
			"locked": false,
			"startBinding": {
				"elementId": "WijvAxx6",
				"focus": -1.3793878506756359,
				"gap": 5.390822366955263
			},
			"endBinding": {
				"elementId": "Ss2RI_KHlx9JToX9bSRy9",
				"gap": 1.355493879007847,
				"focus": 0.08999325624637074
			},
			"lastCommittedPoint": null,
			"startArrowhead": null,
			"endArrowhead": "arrow",
			"points": [
				[
					0,
					0
				],
				[
					14.110644515372014,
					-0.06608807192479067
				]
			]
		},
		{
			"type": "line",
			"version": 1981,
			"versionNonce": 576455759,
			"isDeleted": false,
			"id": "4Pg60yCem3VgfjGnRteZZ",
			"fillStyle": "solid",
			"strokeWidth": 1,
			"strokeStyle": "dotted",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": 3.1295908215216173,
			"y": 84.08303972063018,
			"strokeColor": "#000000",
			"backgroundColor": "#868e96",
			"width": 0.032933835894282115,
			"height": 16.860641405570814,
			"seed": 30776143,
			"groupIds": [
				"Slu1BuXYmob_hgWlngIMh",
				"PF2HmJersAWA4aRaBQ8N6"
			],
			"frameId": null,
			"roundness": {
				"type": 2
			},
			"boundElements": [],
			"updated": 1711505429099,
			"link": null,
			"locked": false,
			"startBinding": null,
			"endBinding": null,
			"lastCommittedPoint": null,
			"startArrowhead": null,
			"endArrowhead": null,
			"points": [
				[
					0,
					0
				],
				[
					0.032933835894282115,
					16.860641405570814
				]
			]
		},
		{
			"type": "line",
			"version": 1875,
			"versionNonce": 1150315553,
			"isDeleted": false,
			"id": "Xfn8bTaV9KL6RgnXT3hKf",
			"fillStyle": "solid",
			"strokeWidth": 1,
			"strokeStyle": "dotted",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": 64.70137111477703,
			"y": 85.63477691819062,
			"strokeColor": "#000000",
			"backgroundColor": "#868e96",
			"width": 0.08245824850372045,
			"height": 15.865000927991385,
			"seed": 1715689839,
			"groupIds": [
				"Slu1BuXYmob_hgWlngIMh",
				"PF2HmJersAWA4aRaBQ8N6"
			],
			"frameId": null,
			"roundness": {
				"type": 2
			},
			"boundElements": [],
			"updated": 1711505429099,
			"link": null,
			"locked": false,
			"startBinding": null,
			"endBinding": null,
			"lastCommittedPoint": null,
			"startArrowhead": null,
			"endArrowhead": null,
			"points": [
				[
					0,
					0
				],
				[
					0.08245824850372045,
					15.865000927991385
				]
			]
		},
		{
			"type": "text",
			"version": 690,
			"versionNonce": 1841631695,
			"isDeleted": false,
			"id": "J3vYSsTg",
			"fillStyle": "solid",
			"strokeWidth": 1,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -2.4767452564805694,
			"y": 61.93305721418497,
			"strokeColor": "#000000",
			"backgroundColor": "transparent",
			"width": 9.855438232421875,
			"height": 8.17817237995874,
			"seed": 244601743,
			"groupIds": [
				"Slu1BuXYmob_hgWlngIMh",
				"PF2HmJersAWA4aRaBQ8N6"
			],
			"frameId": null,
			"roundness": null,
			"boundElements": [
				{
					"type": "arrow",
					"id": "FJLtWDtDULzWS8M-4aDH5"
				},
				{
					"type": "arrow",
					"id": "AadhtsCu7XY-ED6vixQMV"
				}
			],
			"updated": 1711505704291,
			"link": null,
			"locked": false,
			"fontSize": 6.057905466636109,
			"fontFamily": 1,
			"text": "Key",
			"rawText": "",
			"textAlign": "center",
			"verticalAlign": "middle",
			"containerId": null,
			"originalText": "Key",
			"lineHeight": 1.3499999999999988,
			"baseline": 5
		},
		{
			"type": "text",
			"version": 763,
			"versionNonce": 170456737,
			"isDeleted": false,
			"id": "pRNFkKzs",
			"fillStyle": "solid",
			"strokeWidth": 1,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -1.870954709819614,
			"y": 102.06639896640914,
			"strokeColor": "#000000",
			"backgroundColor": "transparent",
			"width": 9.855438232421875,
			"height": 8.17817237995874,
			"seed": 318835119,
			"groupIds": [
				"Slu1BuXYmob_hgWlngIMh",
				"PF2HmJersAWA4aRaBQ8N6"
			],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1711505704291,
			"link": null,
			"locked": false,
			"fontSize": 6.057905466636109,
			"fontFamily": 1,
			"text": "Key",
			"rawText": "",
			"textAlign": "center",
			"verticalAlign": "middle",
			"containerId": null,
			"originalText": "Key",
			"lineHeight": 1.3499999999999988,
			"baseline": 5
		},
		{
			"type": "text",
			"version": 662,
			"versionNonce": 1107296239,
			"isDeleted": false,
			"id": "m35ZUkP8",
			"fillStyle": "solid",
			"strokeWidth": 1,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": 55.20538883497608,
			"y": 62.22630086249288,
			"strokeColor": "#000000",
			"backgroundColor": "transparent",
			"width": 15.500045776367188,
			"height": 8.17817237995874,
			"seed": 1890712527,
			"groupIds": [
				"Slu1BuXYmob_hgWlngIMh",
				"PF2HmJersAWA4aRaBQ8N6"
			],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1711505704291,
			"link": null,
			"locked": false,
			"fontSize": 6.057905466636125,
			"fontFamily": 1,
			"text": "Value",
			"rawText": "",
			"textAlign": "center",
			"verticalAlign": "middle",
			"containerId": null,
			"originalText": "Value",
			"lineHeight": 1.3499999999999952,
			"baseline": 5
		},
		{
			"type": "text",
			"version": 769,
			"versionNonce": 1576237697,
			"isDeleted": false,
			"id": "FHFe9uIa",
			"fillStyle": "solid",
			"strokeWidth": 1,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": 54.9024935616481,
			"y": 102.77190107207153,
			"strokeColor": "#000000",
			"backgroundColor": "transparent",
			"width": 15.500045776367188,
			"height": 8.17817237995874,
			"seed": 1807722991,
			"groupIds": [
				"Slu1BuXYmob_hgWlngIMh",
				"PF2HmJersAWA4aRaBQ8N6"
			],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1711505704291,
			"link": null,
			"locked": false,
			"fontSize": 6.057905466636125,
			"fontFamily": 1,
			"text": "Value",
			"rawText": "",
			"textAlign": "center",
			"verticalAlign": "middle",
			"containerId": null,
			"originalText": "Value",
			"lineHeight": 1.3499999999999952,
			"baseline": 5
		},
		{
			"type": "text",
			"version": 916,
			"versionNonce": 1224223247,
			"isDeleted": false,
			"id": "WijvAxx6",
			"fillStyle": "solid",
			"strokeWidth": 1,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": 11.072006511001064,
			"y": 112.58477238766355,
			"strokeColor": "#000000",
			"backgroundColor": "transparent",
			"width": 62.87358093261719,
			"height": 27.976292259030313,
			"seed": 825398287,
			"groupIds": [
				"PF2HmJersAWA4aRaBQ8N6"
			],
			"frameId": null,
			"roundness": null,
			"boundElements": [
				{
					"type": "arrow",
					"id": "vOHLflugLaWsyIDboF8jJ"
				}
			],
			"updated": 1711505704292,
			"link": null,
			"locked": false,
			"fontSize": 22.0359584435366,
			"fontFamily": 1,
			"text": "Cache",
			"rawText": "",
			"textAlign": "center",
			"verticalAlign": "top",
			"containerId": null,
			"originalText": "Cache",
			"lineHeight": 1.269574560630744,
			"baseline": 19
		},
		{
			"id": "mMK6u1slZDB417Rym_362",
			"type": "arrow",
			"x": -68.90177299037636,
			"y": -10.120225923665252,
			"width": 55.1616832360753,
			"height": 51.71449210424662,
			"angle": 0,
			"strokeColor": "#1e1e1e",
			"backgroundColor": "#e9ecef",
			"fillStyle": "solid",
			"strokeWidth": 1,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"seed": 1870204961,
			"version": 152,
			"versionNonce": 1837744943,
			"isDeleted": false,
			"boundElements": null,
			"updated": 1711505429099,
			"link": null,
			"locked": false,
			"points": [
				[
					0,
					0
				],
				[
					55.1616832360753,
					51.71449210424662
				]
			],
			"lastCommittedPoint": [
				39.34275347037942,
				36.391503698205554
			],
			"startBinding": {
				"elementId": "_Ctghe3Vio8d5qrkqE_2e",
				"focus": 0.3219903337282327,
				"gap": 12.177282617162497
			},
			"endBinding": {
				"elementId": "FB58yCOt_UJaZ_TkmPGoT",
				"focus": 0.03529977295987467,
				"gap": 12.165177405863375
			},
			"startArrowhead": null,
			"endArrowhead": "arrow"
		},
		{
			"id": "CzoMex3ErycdVWThqPyq9",
			"type": "arrow",
			"x": 100.61194094122959,
			"y": 43.45635353011434,
			"width": 33.75680716157899,
			"height": 29.885938279450357,
			"angle": 0,
			"strokeColor": "#1e1e1e",
			"backgroundColor": "#e9ecef",
			"fillStyle": "solid",
			"strokeWidth": 1,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"seed": 314197633,
			"version": 277,
			"versionNonce": 1531611969,
			"isDeleted": false,
			"boundElements": null,
			"updated": 1711505429099,
			"link": null,
			"locked": false,
			"points": [
				[
					0,
					0
				],
				[
					33.75680716157899,
					-29.885938279450357
				]
			],
			"lastCommittedPoint": [
				27.07453489216209,
				-18.266594292249238
			],
			"startBinding": {
				"elementId": "FB58yCOt_UJaZ_TkmPGoT",
				"focus": -0.03680458969760378,
				"gap": 10.303090056330404
			},
			"endBinding": {
				"elementId": "ndbbminG",
				"focus": -0.188506463915012,
				"gap": 3.7211124740686827
			},
			"startArrowhead": null,
			"endArrowhead": "arrow"
		},
		{
			"id": "QO0RSRKg",
			"type": "text",
			"x": -39.3540447253049,
			"y": 147.57641749999152,
			"width": 179.56788635253906,
			"height": 60,
			"angle": 0,
			"strokeColor": "#1e1e1e",
			"backgroundColor": "#e9ecef",
			"fillStyle": "solid",
			"strokeWidth": 1,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"seed": 1995758465,
			"version": 123,
			"versionNonce": 266228737,
			"isDeleted": false,
			"boundElements": null,
			"updated": 1711505452692,
			"link": null,
			"locked": false,
			"text": "Very popular pastes\ncan be cached to\nreduce database load.",
			"rawText": "Very popular pastes\ncan be cached to\nreduce database load.",
			"fontSize": 16,
			"fontFamily": 1,
			"textAlign": "left",
			"verticalAlign": "top",
			"baseline": 54,
			"containerId": null,
			"originalText": "Very popular pastes\ncan be cached to\nreduce database load.",
			"lineHeight": 1.25
		},
		{
			"type": "rectangle",
			"version": 1302,
			"versionNonce": 724497345,
			"isDeleted": true,
			"id": "cdSlgEz0zcZ9Yc5184oW6",
			"fillStyle": "solid",
			"strokeWidth": 1,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -129.6512533779385,
			"y": -355.53355524457595,
			"strokeColor": "#000000",
			"backgroundColor": "#eeeeee",
			"width": 96.04882870779743,
			"height": 94.20173584803199,
			"seed": 2029147375,
			"groupIds": [
				"QS2wD7AJwgNYtxDS0Jokd"
			],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1711505429099,
			"link": null,
			"locked": false
		},
		{
			"type": "text",
			"version": 712,
			"versionNonce": 440132815,
			"isDeleted": true,
			"id": "kEQNzK6H",
			"fillStyle": "solid",
			"strokeWidth": 1,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -119.530433994743,
			"y": -328.5164201866311,
			"strokeColor": "#000000",
			"backgroundColor": "#ced4da",
			"width": 75.80718994140625,
			"height": 40.167465732141956,
			"seed": 2027413263,
			"groupIds": [
				"QS2wD7AJwgNYtxDS0Jokd"
			],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1711505429099,
			"link": null,
			"locked": false,
			"fontSize": 14.876839160052583,
			"fontFamily": 1,
			"text": "Application\nserver",
			"rawText": "Application\nserver",
			"textAlign": "center",
			"verticalAlign": "top",
			"containerId": null,
			"originalText": "Application\nserver",
			"lineHeight": 1.3499999999999994,
			"baseline": 33
		},
		{
			"type": "rectangle",
			"version": 1414,
			"versionNonce": 595383201,
			"isDeleted": true,
			"id": "ICM3-V3f-AR66MEWW4w1z",
			"fillStyle": "solid",
			"strokeWidth": 1,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -119.6512533779385,
			"y": -345.53355524457595,
			"strokeColor": "#000000",
			"backgroundColor": "#eeeeee",
			"width": 96.04882870779743,
			"height": 94.20173584803199,
			"seed": 2028923663,
			"groupIds": [
				"BCULs3I5y44cX6LHg0sZ1"
			],
			"frameId": null,
			"roundness": null,
			"boundElements": null,
			"updated": 1711505429099,
			"link": null,
			"locked": false
		},
		{
			"type": "text",
			"version": 1030,
			"versionNonce": 2116317935,
			"isDeleted": true,
			"id": "oYxbVtKp",
			"fillStyle": "solid",
			"strokeWidth": 1,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -118.89881168028988,
			"y": -331.49971603336576,
			"strokeColor": "#000000",
			"backgroundColor": "#ced4da",
			"width": 94.5439453125,
			"height": 64.79999999999997,
			"seed": 34885985,
			"groupIds": [
				"BCULs3I5y44cX6LHg0sZ1"
			],
			"frameId": null,
			"roundness": null,
			"boundElements": null,
			"updated": 1711505429099,
			"link": null,
			"locked": false,
			"fontSize": 16,
			"fontFamily": 1,
			"text": "Distributed\nCoordination\nService",
			"rawText": "Distributed\nCoordination\nService",
			"textAlign": "center",
			"verticalAlign": "top",
			"containerId": null,
			"originalText": "Distributed\nCoordination\nService",
			"lineHeight": 1.3499999999999994,
			"baseline": 57
		},
		{
			"id": "URtbIRwq",
			"type": "text",
			"x": -448.814687062654,
			"y": 58.45086050155601,
			"width": 8,
			"height": 20,
			"angle": 0,
			"strokeColor": "#1e1e1e",
			"backgroundColor": "#e9ecef",
			"fillStyle": "solid",
			"strokeWidth": 1,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"seed": 1280814575,
			"version": 7,
			"versionNonce": 985905025,
			"isDeleted": true,
			"boundElements": null,
			"updated": 1711505429099,
			"link": null,
			"locked": false,
			"text": "",
			"rawText": "",
			"fontSize": 16,
			"fontFamily": 1,
			"textAlign": "left",
			"verticalAlign": "top",
			"baseline": 14,
			"containerId": null,
			"originalText": "",
			"lineHeight": 1.25
		},
		{
			"id": "MKeuUXvq",
			"type": "text",
			"x": -107.13440452376068,
			"y": -338.7366692472888,
			"width": 8,
			"height": 20,
			"angle": 0,
			"strokeColor": "#1e1e1e",
			"backgroundColor": "#e9ecef",
			"fillStyle": "solid",
			"strokeWidth": 1,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"seed": 183274031,
			"version": 5,
			"versionNonce": 236338447,
			"isDeleted": true,
			"boundElements": null,
			"updated": 1711505429099,
			"link": null,
			"locked": false,
			"text": "",
			"rawText": "",
			"fontSize": 16,
			"fontFamily": 1,
			"textAlign": "left",
			"verticalAlign": "top",
			"baseline": 14,
			"containerId": null,
			"originalText": "",
			"lineHeight": 1.25
		},
		{
			"id": "6ZCT89zx",
			"type": "text",
			"x": -98.90225821097229,
			"y": -205.49972851752833,
			"width": 8,
			"height": 20,
			"angle": 0,
			"strokeColor": "#1e1e1e",
			"backgroundColor": "#e9ecef",
			"fillStyle": "solid",
			"strokeWidth": 1,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"seed": 610943841,
			"version": 5,
			"versionNonce": 860036961,
			"isDeleted": true,
			"boundElements": null,
			"updated": 1711505429099,
			"link": null,
			"locked": false,
			"text": "",
			"rawText": "",
			"fontSize": 16,
			"fontFamily": 1,
			"textAlign": "center",
			"verticalAlign": "middle",
			"baseline": 14,
			"containerId": "JLcBC_Je1UCxJ5-PfPWqi",
			"originalText": "",
			"lineHeight": 1.25
		}
	],
	"appState": {
		"theme": "dark",
		"viewBackgroundColor": "#ffffff",
		"currentItemStrokeColor": "#1e1e1e",
		"currentItemBackgroundColor": "#e9ecef",
		"currentItemFillStyle": "solid",
		"currentItemStrokeWidth": 1,
		"currentItemStrokeStyle": "solid",
		"currentItemRoughness": 1,
		"currentItemOpacity": 100,
		"currentItemFontFamily": 1,
		"currentItemFontSize": 16,
		"currentItemTextAlign": "left",
		"currentItemStartArrowhead": null,
		"currentItemEndArrowhead": "arrow",
		"scrollX": 1266.936691104972,
		"scrollY": 796.5366578202681,
		"zoom": {
			"value": 0.978083618531485
		},
		"currentItemRoundness": "sharp",
		"gridSize": null,
		"gridColor": {
			"Bold": "#C9C9C9FF",
			"Regular": "#EDEDEDFF"
		},
		"currentStrokeOptions": null,
		"previousGridSize": null,
		"frameRendering": {
			"enabled": true,
			"clip": true,
			"name": true,
			"outline": true
		}
	},
	"files": {}
}
```
%%