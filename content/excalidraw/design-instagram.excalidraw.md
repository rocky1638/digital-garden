---

excalidraw-plugin: parsed
tags: [excalidraw]

---
==⚠  Switch to EXCALIDRAW VIEW in the MORE OPTIONS menu of this document. ⚠==


# Text Elements
Instagram ^46SBldcx

Lorem ipsum dolor sit amet, 
consectetur adipiscing elit,sed
 do eiusmod tempor incididunt
 ut labore et dolore magna
 aliqua. Ut enim ad miveniam,
 quis nostrud exercitaullamco 
laboris nisi ut aliquip ex ea 
ommodo consequat. Duis aute 
irure dolor in reprehenderit i ^LMbrEp4p

Lorem ipsum dolor s, 
consectetur adipng d
 do eiusmopor incididunt
ut labore et dolore magna
aliqua. Ut enim ad miveniam,
quis nostrud exercitaullamco 
laboris nisi ut aliquip ex ea 
ommodo consequat. Duis aute 
 ^IUINTUJp

Application
server ^zAcMeEmY

upload image ^LzPNdTYJ

save image ^sUYQjlIY

Possible extensions:

- Device could do compression before sending
  photo to the server.
- More details on how to handle sharding. ^Mmz7Xppu

posts ^eaUTk4w5

image_link: url
user_id: ID
created_at: timestamp
description: str

 ^SMVgfOhz

save metadata ^xiFuli21

follow user ^P81NgQkP

Graph DB ^zGOEJ1HC

store
follower
relationship ^6w0NP3bW

each user vertex
has indegrees from people
that are following them
and outdegrees to people
that they follow. ^3CPse1W4

How to get the feed for a user?

1. Get all the users that the user is following.
2. Grab 50 most recent posts from all those users.
3. Send list of posts back to the user.
4. User can make requests to download actual
   image files on a scrolling basis.

How to implement?

Push:

- Have a feed generation service that listens for
  new images posted, and then performs the above
  steps, writing the post_id to each follower's feed
  in the cache.
- This has the downside that for users with millions
  of followers, millions of updates will need to be made
  to our feed cache when they upload a photo.

Pull:

- For celebrities, we can instead just have users pull
  the new photo_ids when they go to view their feed.
- This way, there isn't an immediate spike when a celebrity
  posts a photo.
- We could maintain a list/filter of accounts that should
  use this "pull" paradigm instead of push; could be something
  as simple as if they have >100K followers.

 ^0vnesiXj

Feed Generation
Service ^5BRT2oe3

user ids
are shared ^BlEy0jz0

request feed ^CREfdNuX

computed feeds ^sOdNYvJL

Key ^Z6GYremN

Key ^eJnyr4vf

Value ^JQ9449Io

Value ^VMxkYEPI

Cache ^komHsex0

listen to 
image writes ^lfs0JnJB

find all followers
who need to have this
image in their feed ^c3NY1JvM

write post_id
to correct feeds ^8QCAbsAq

Load
Balancer ^x0tgiCgj

Application
server ^F8PpsgnZ

replicate object storage for durability

shard photo storage by geography,
because most access patterns are
likely geographically bound. ^vxLVdkeq

Feed Generation
Service ^Ip4sLVub

CDN ^e7WSgP64

User checks CDN
first for photo.
On a cache miss,
grab from object store
and write back-through
into the CDN cache. ^OtRBWdT9

cache recent
posts locally
on device. ^8CMrt2ku

%%
# Drawing
```json
{
	"type": "excalidraw",
	"version": 2,
	"source": "https://github.com/zsviczian/obsidian-excalidraw-plugin/releases/tag/2.0.25",
	"elements": [
		{
			"type": "text",
			"version": 749,
			"versionNonce": 155845752,
			"isDeleted": false,
			"id": "46SBldcx",
			"fillStyle": "solid",
			"strokeWidth": 1,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 80,
			"angle": 0,
			"x": 129.37653117627235,
			"y": 634.3370548560418,
			"strokeColor": "#000000",
			"backgroundColor": "#ced4da",
			"width": 80.23774719238281,
			"height": 20.41793446832189,
			"seed": 653076344,
			"groupIds": [
				"I_wrY3yW5VkiRANBg1lTR"
			],
			"frameId": null,
			"roundness": null,
			"boundElements": [
				{
					"id": "fscKPB-NVypfeIpnDLz5P",
					"type": "arrow"
				}
			],
			"updated": 1711591447173,
			"link": null,
			"locked": false,
			"fontSize": 15.990384459685862,
			"fontFamily": 1,
			"text": "Instagram",
			"rawText": "Instagram",
			"textAlign": "center",
			"verticalAlign": "top",
			"containerId": null,
			"originalText": "Instagram",
			"lineHeight": 1.276888277439391,
			"baseline": 14
		},
		{
			"type": "rectangle",
			"version": 1676,
			"versionNonce": 410494216,
			"isDeleted": false,
			"id": "Fp4GUsYjbYsT-oeTxBm9a",
			"fillStyle": "solid",
			"strokeWidth": 1,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 80,
			"angle": 0,
			"x": 127.19426511346944,
			"y": 502.9077246801527,
			"strokeColor": "#000000",
			"backgroundColor": "#ced4da",
			"width": 84.60227931798867,
			"height": 129.38788619865684,
			"seed": 1456044152,
			"groupIds": [
				"hHpxRbaWOi8m-ftuiEbtv",
				"I_wrY3yW5VkiRANBg1lTR"
			],
			"frameId": null,
			"roundness": {
				"type": 1
			},
			"boundElements": [
				{
					"id": "zz4n1wx0QcbUHZHH6NdMp",
					"type": "arrow"
				}
			],
			"updated": 1711590624831,
			"link": null,
			"locked": false
		},
		{
			"type": "rectangle",
			"version": 1897,
			"versionNonce": 1544028936,
			"isDeleted": false,
			"id": "5bYSm2V2fEX5_z-MuwxYP",
			"fillStyle": "solid",
			"strokeWidth": 1,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 80,
			"angle": 0,
			"x": 131.12736627109177,
			"y": 507.445913930634,
			"strokeColor": "#000000",
			"backgroundColor": "#fff",
			"width": 75.86866432368348,
			"height": 120.70738781243189,
			"seed": 1223928184,
			"groupIds": [
				"hHpxRbaWOi8m-ftuiEbtv",
				"I_wrY3yW5VkiRANBg1lTR"
			],
			"frameId": null,
			"roundness": {
				"type": 1
			},
			"boundElements": [
				{
					"id": "OYX5n8TJFSoUeiR6gmBqV",
					"type": "arrow"
				},
				{
					"id": "mdmXmJQX9zIgdEWBkjYyq",
					"type": "arrow"
				}
			],
			"updated": 1711590624831,
			"link": null,
			"locked": false
		},
		{
			"type": "ellipse",
			"version": 1910,
			"versionNonce": 1961328648,
			"isDeleted": false,
			"id": "Qe6odqSdKLpf1_s00YeIs",
			"fillStyle": "solid",
			"strokeWidth": 1,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 80,
			"angle": 0,
			"x": 167.38085833653884,
			"y": 506.3297285652318,
			"strokeColor": "#000000",
			"backgroundColor": "#fff",
			"width": 5.218983964155919,
			"height": 5.218983964155919,
			"seed": 951040632,
			"groupIds": [
				"hHpxRbaWOi8m-ftuiEbtv",
				"I_wrY3yW5VkiRANBg1lTR"
			],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1711590624831,
			"link": null,
			"locked": false
		},
		{
			"type": "rectangle",
			"version": 1564,
			"versionNonce": 1124744968,
			"isDeleted": false,
			"id": "oZbikZGCO7n6A21d81A0t",
			"fillStyle": "cross-hatch",
			"strokeWidth": 1,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 80,
			"angle": 0,
			"x": 134.69064133747486,
			"y": 516.1644317463536,
			"strokeColor": "#000000",
			"backgroundColor": "#15aabf",
			"width": 68.16682121289108,
			"height": 31.815443659489233,
			"seed": 1489087352,
			"groupIds": [
				"hHpxRbaWOi8m-ftuiEbtv",
				"I_wrY3yW5VkiRANBg1lTR"
			],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1711590624831,
			"link": null,
			"locked": false
		},
		{
			"type": "rectangle",
			"version": 1593,
			"versionNonce": 1551703560,
			"isDeleted": false,
			"id": "KiWv9uu5ag13zSpobqe3J",
			"fillStyle": "cross-hatch",
			"strokeWidth": 1,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 80,
			"angle": 0,
			"x": 139.29298516146298,
			"y": 554.617170498022,
			"strokeColor": "#000000",
			"backgroundColor": "#fab005",
			"width": 23.86926190701229,
			"height": 18.583705165525398,
			"seed": 1668119672,
			"groupIds": [
				"hHpxRbaWOi8m-ftuiEbtv",
				"I_wrY3yW5VkiRANBg1lTR"
			],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1711590624831,
			"link": null,
			"locked": false
		},
		{
			"type": "rectangle",
			"version": 1642,
			"versionNonce": 574364936,
			"isDeleted": false,
			"id": "6odww_uFGe4oBKejSwzI5",
			"fillStyle": "cross-hatch",
			"strokeWidth": 1,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 80,
			"angle": 0,
			"x": 177.4748337014388,
			"y": 590.2276712377035,
			"strokeColor": "#000000",
			"backgroundColor": "#fab005",
			"width": 21.568089995018592,
			"height": 15.707240275533275,
			"seed": 712453496,
			"groupIds": [
				"hHpxRbaWOi8m-ftuiEbtv",
				"I_wrY3yW5VkiRANBg1lTR"
			],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1711590624831,
			"link": null,
			"locked": false
		},
		{
			"type": "text",
			"version": 589,
			"versionNonce": 1975729160,
			"isDeleted": false,
			"id": "LMbrEp4p",
			"fillStyle": "hachure",
			"strokeWidth": 1,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 80,
			"angle": 0,
			"x": 167.54833149100557,
			"y": 552.9371129707638,
			"strokeColor": "#495057",
			"backgroundColor": "transparent",
			"width": 38.119110107421875,
			"height": 31.06582081191504,
			"seed": 656588408,
			"groupIds": [
				"hHpxRbaWOi8m-ftuiEbtv",
				"I_wrY3yW5VkiRANBg1lTR"
			],
			"frameId": null,
			"roundness": {
				"type": 2
			},
			"boundElements": [],
			"updated": 1711590624831,
			"link": null,
			"locked": false,
			"fontSize": 2.518381124150024,
			"fontFamily": 1,
			"text": "Lorem ipsum dolor sit amet, \nconsectetur adipiscing elit,sed\n do eiusmod tempor incididunt\n ut labore et dolore magna\n aliqua. Ut enim ad miveniam,\n quis nostrud exercitaullamco \nlaboris nisi ut aliquip ex ea \nommodo consequat. Duis aute \nirure dolor in reprehenderit i",
			"rawText": "",
			"textAlign": "left",
			"verticalAlign": "top",
			"containerId": null,
			"originalText": "Lorem ipsum dolor sit amet, \nconsectetur adipiscing elit,sed\n do eiusmod tempor incididunt\n ut labore et dolore magna\n aliqua. Ut enim ad miveniam,\n quis nostrud exercitaullamco \nlaboris nisi ut aliquip ex ea \nommodo consequat. Duis aute \nirure dolor in reprehenderit i",
			"lineHeight": 1.3706256908018875,
			"baseline": 30
		},
		{
			"type": "text",
			"version": 632,
			"versionNonce": 688814856,
			"isDeleted": false,
			"id": "IUINTUJp",
			"fillStyle": "hachure",
			"strokeWidth": 1,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 80,
			"angle": 0,
			"x": 136.1948641900907,
			"y": 578.2336836345244,
			"strokeColor": "#495057",
			"backgroundColor": "transparent",
			"width": 38.119110107421875,
			"height": 31.06582081191504,
			"seed": 171192184,
			"groupIds": [
				"hHpxRbaWOi8m-ftuiEbtv",
				"I_wrY3yW5VkiRANBg1lTR"
			],
			"frameId": null,
			"roundness": {
				"type": 2
			},
			"boundElements": [],
			"updated": 1711590624831,
			"link": null,
			"locked": false,
			"fontSize": 2.518381124150024,
			"fontFamily": 1,
			"text": "Lorem ipsum dolor s, \nconsectetur adipng d\n do eiusmopor incididunt\nut labore et dolore magna\naliqua. Ut enim ad miveniam,\nquis nostrud exercitaullamco \nlaboris nisi ut aliquip ex ea \nommodo consequat. Duis aute \n",
			"rawText": "",
			"textAlign": "left",
			"verticalAlign": "top",
			"containerId": null,
			"originalText": "Lorem ipsum dolor s, \nconsectetur adipng d\n do eiusmopor incididunt\nut labore et dolore magna\naliqua. Ut enim ad miveniam,\nquis nostrud exercitaullamco \nlaboris nisi ut aliquip ex ea \nommodo consequat. Duis aute \n",
			"lineHeight": 1.3706256908018875,
			"baseline": 30
		},
		{
			"type": "rectangle",
			"version": 1695,
			"versionNonce": 1855576584,
			"isDeleted": false,
			"id": "7BTXMoJpgp1GOEDxNO7iY",
			"fillStyle": "cross-hatch",
			"strokeWidth": 1,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": 135.3427970993788,
			"y": 610.3664735880691,
			"strokeColor": "#000000",
			"backgroundColor": "#15aabf",
			"width": 68.16682121289108,
			"height": 10.953641050551655,
			"seed": 1273987192,
			"groupIds": [
				"hHpxRbaWOi8m-ftuiEbtv",
				"I_wrY3yW5VkiRANBg1lTR"
			],
			"frameId": null,
			"roundness": {
				"type": 1
			},
			"boundElements": [],
			"updated": 1711590624831,
			"link": null,
			"locked": false
		},
		{
			"type": "rectangle",
			"version": 1505,
			"versionNonce": 2105462136,
			"isDeleted": false,
			"id": "NE7r0GWkhpC_qgDFN63wO",
			"fillStyle": "solid",
			"strokeWidth": 1,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": 574.8121837744079,
			"y": 521.7791510583505,
			"strokeColor": "#000000",
			"backgroundColor": "#eeeeee",
			"width": 96.04882870779743,
			"height": 94.20173584803199,
			"seed": 116158072,
			"groupIds": [
				"WJoI1FeN75XB3an_638zh"
			],
			"frameId": null,
			"roundness": null,
			"boundElements": [
				{
					"id": "90Jm58sKkmgEgnFMewqoO",
					"type": "arrow"
				},
				{
					"id": "pAgjnBHfyGmYu6uyJq2Ke",
					"type": "arrow"
				},
				{
					"id": "t5cnS97ON8dGAg6wFa1nb",
					"type": "arrow"
				},
				{
					"id": "cBmfK-bBHpP80_3GqBKEF",
					"type": "arrow"
				},
				{
					"id": "X9vAp0L3eWEitFELhVhsM",
					"type": "arrow"
				}
			],
			"updated": 1711590642499,
			"link": null,
			"locked": false
		},
		{
			"type": "text",
			"version": 903,
			"versionNonce": 630613624,
			"isDeleted": false,
			"id": "zAcMeEmY",
			"fillStyle": "solid",
			"strokeWidth": 1,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": 584.9006582701725,
			"y": 548.7962861162954,
			"strokeColor": "#000000",
			"backgroundColor": "#ced4da",
			"width": 75.87187971626813,
			"height": 40.167465732141956,
			"seed": 625467256,
			"groupIds": [
				"WJoI1FeN75XB3an_638zh"
			],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1711590642502,
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
			"baseline": 34
		},
		{
			"type": "rectangle",
			"version": 1507,
			"versionNonce": 556243832,
			"isDeleted": false,
			"id": "CnSQZuPZVa17A40oRGiea",
			"fillStyle": "solid",
			"strokeWidth": 1,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": 584.8121837744079,
			"y": 531.7791510583505,
			"strokeColor": "#000000",
			"backgroundColor": "#eeeeee",
			"width": 96.04882870779743,
			"height": 94.20173584803199,
			"seed": 1122139144,
			"groupIds": [
				"U8tbZoGlO1V7NJiWQwHR8"
			],
			"frameId": null,
			"roundness": null,
			"boundElements": [
				{
					"id": "90Jm58sKkmgEgnFMewqoO",
					"type": "arrow"
				},
				{
					"id": "t5cnS97ON8dGAg6wFa1nb",
					"type": "arrow"
				}
			],
			"updated": 1711590655126,
			"link": null,
			"locked": false
		},
		{
			"type": "text",
			"version": 904,
			"versionNonce": 600525832,
			"isDeleted": false,
			"id": "F8PpsgnZ",
			"fillStyle": "solid",
			"strokeWidth": 1,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": 594.9006582701725,
			"y": 558.7962861162954,
			"strokeColor": "#000000",
			"backgroundColor": "#ced4da",
			"width": 75.87187971626813,
			"height": 40.167465732141956,
			"seed": 798566520,
			"groupIds": [
				"U8tbZoGlO1V7NJiWQwHR8"
			],
			"frameId": null,
			"roundness": null,
			"boundElements": [
				{
					"id": "t5cnS97ON8dGAg6wFa1nb",
					"type": "arrow"
				}
			],
			"updated": 1711590653681,
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
			"baseline": 34
		},
		{
			"id": "OYX5n8TJFSoUeiR6gmBqV",
			"type": "arrow",
			"x": 224.62035495692146,
			"y": 568.0112789022504,
			"width": 208.33771911188205,
			"height": 0,
			"angle": 0,
			"strokeColor": "#1e1e1e",
			"backgroundColor": "transparent",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"groupIds": [],
			"frameId": null,
			"roundness": {
				"type": 2
			},
			"seed": 23491192,
			"version": 464,
			"versionNonce": 1003351048,
			"isDeleted": false,
			"boundElements": [
				{
					"type": "text",
					"id": "LzPNdTYJ"
				}
			],
			"updated": 1711590632156,
			"link": null,
			"locked": false,
			"points": [
				[
					0,
					0
				],
				[
					208.33771911188205,
					0
				]
			],
			"lastCommittedPoint": [
				173.59284113459574,
				0
			],
			"startBinding": {
				"elementId": "5bYSm2V2fEX5_z-MuwxYP",
				"focus": 0.0035071766399162683,
				"gap": 17.624324362146226
			},
			"endBinding": {
				"elementId": "ql6LG2EuU-F-mYLltKJvg",
				"focus": -0.043967451664626414,
				"gap": 8.349458611067917
			},
			"startArrowhead": null,
			"endArrowhead": "arrow"
		},
		{
			"id": "LzPNdTYJ",
			"type": "text",
			"x": 419.5155750038204,
			"y": 558.0112789022504,
			"width": 98.89593505859375,
			"height": 20,
			"angle": 0,
			"strokeColor": "#1e1e1e",
			"backgroundColor": "transparent",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"seed": 244086904,
			"version": 37,
			"versionNonce": 1019642232,
			"isDeleted": false,
			"boundElements": null,
			"updated": 1711589210629,
			"link": null,
			"locked": false,
			"text": "upload image",
			"rawText": "upload image",
			"fontSize": 16,
			"fontFamily": 1,
			"textAlign": "center",
			"verticalAlign": "middle",
			"baseline": 14,
			"containerId": "OYX5n8TJFSoUeiR6gmBqV",
			"originalText": "upload image",
			"lineHeight": 1.25
		},
		{
			"type": "line",
			"version": 6485,
			"versionNonce": 1605821192,
			"isDeleted": false,
			"id": "3pQiQrAfaVsR_dPT6IzmW",
			"fillStyle": "solid",
			"strokeWidth": 1,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": 883.6271187686672,
			"y": 541.3747016750831,
			"strokeColor": "#000000",
			"backgroundColor": "#ced4da",
			"width": 71.66451803756424,
			"height": 92.4944378166419,
			"seed": 1190756472,
			"groupIds": [
				"mvGMS62Dwv7bvFIDCGdjv",
				"7i4WOHhMpzy8J4zPo1_Z7",
				"11KAHy1xbRp8g0PEz8N5v",
				"3D7FOAwyMVuxnZrYz7c2H"
			],
			"frameId": null,
			"roundness": {
				"type": 2
			},
			"boundElements": null,
			"updated": 1711590984704,
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
					0.23631277756161562,
					69.90679477501719
				],
				[
					0.011058883236775303,
					77.86537979260234
				],
				[
					3.690881175524461,
					81.30418596549401
				],
				[
					16.505678697187165,
					84.21452947378963
				],
				[
					38.166316523905,
					85.12076696651043
				],
				[
					58.86162358869831,
					83.67382606057318
				],
				[
					69.85719260843815,
					80.2134930539004
				],
				[
					71.40796883026277,
					77.29639602912391
				],
				[
					71.62576973675768,
					70.88899726829273
				],
				[
					71.45482135084606,
					5.864789891179346
				],
				[
					71.06944881668004,
					-0.27879963213419856
				],
				[
					66.4678637859641,
					-3.712492230559498
				],
				[
					56.77790772977523,
					-5.70110529183138
				],
				[
					34.69580711193442,
					-7.373670850131469
				],
				[
					16.99156283916344,
					-6.376316241616809
				],
				[
					3.0672949545182333,
					-2.9934111019973204
				],
				[
					-0.038748300806571497,
					-0.04200446053826079
				],
				[
					0,
					0
				]
			]
		},
		{
			"type": "ellipse",
			"version": 7313,
			"versionNonce": 66404872,
			"isDeleted": false,
			"id": "nOvMCGK0jawtK74iK2Gs4",
			"fillStyle": "solid",
			"strokeWidth": 1,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": 883.7776238145804,
			"y": 534.1665314120553,
			"strokeColor": "#000000",
			"backgroundColor": "#fff",
			"width": 71.20485008239825,
			"height": 14.40064523308222,
			"seed": 1172484472,
			"groupIds": [
				"mvGMS62Dwv7bvFIDCGdjv",
				"7i4WOHhMpzy8J4zPo1_Z7",
				"11KAHy1xbRp8g0PEz8N5v",
				"3D7FOAwyMVuxnZrYz7c2H"
			],
			"frameId": null,
			"roundness": null,
			"boundElements": null,
			"updated": 1711590984704,
			"link": null,
			"locked": false
		},
		{
			"type": "diamond",
			"version": 1578,
			"versionNonce": 1863303432,
			"isDeleted": false,
			"id": "psY6ixsR9bwqnI-Vry7Ye",
			"fillStyle": "solid",
			"strokeWidth": 1,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": 926.1040332882263,
			"y": 555.856944694815,
			"strokeColor": "#000000",
			"backgroundColor": "#868e96",
			"width": 22.14493603658657,
			"height": 25.74992562393783,
			"seed": 1383973496,
			"groupIds": [
				"7i4WOHhMpzy8J4zPo1_Z7",
				"11KAHy1xbRp8g0PEz8N5v",
				"3D7FOAwyMVuxnZrYz7c2H"
			],
			"frameId": null,
			"roundness": null,
			"boundElements": null,
			"updated": 1711590984704,
			"link": null,
			"locked": false
		},
		{
			"type": "ellipse",
			"version": 1785,
			"versionNonce": 813850632,
			"isDeleted": false,
			"id": "3KL98VGmQJ6XJ2qXCOtoM",
			"fillStyle": "solid",
			"strokeWidth": 1,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": 913.7440689887338,
			"y": 594.9968316432008,
			"strokeColor": "#000000",
			"backgroundColor": "#868e96",
			"width": 23.68993157402284,
			"height": 22.659934549065266,
			"seed": 462336888,
			"groupIds": [
				"7i4WOHhMpzy8J4zPo1_Z7",
				"11KAHy1xbRp8g0PEz8N5v",
				"3D7FOAwyMVuxnZrYz7c2H"
			],
			"frameId": null,
			"roundness": null,
			"boundElements": null,
			"updated": 1711590984704,
			"link": null,
			"locked": false
		},
		{
			"type": "line",
			"version": 3116,
			"versionNonce": 139009800,
			"isDeleted": false,
			"id": "phSnhLxDEdU8HRKEoArqZ",
			"fillStyle": "solid",
			"strokeWidth": 1,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": 902.8871415025312,
			"y": 569.1584815620441,
			"strokeColor": "#000000",
			"backgroundColor": "#868e96",
			"width": 21.517963614269437,
			"height": 19.662074531243835,
			"seed": 1465484408,
			"groupIds": [
				"7i4WOHhMpzy8J4zPo1_Z7",
				"11KAHy1xbRp8g0PEz8N5v",
				"3D7FOAwyMVuxnZrYz7c2H"
			],
			"frameId": null,
			"roundness": null,
			"boundElements": null,
			"updated": 1711590984704,
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
					10.48483163908686,
					19.662074531243835
				],
				[
					-11.03313197518258,
					19.42132297980718
				],
				[
					0,
					0
				]
			]
		},
		{
			"type": "line",
			"version": 6677,
			"versionNonce": 222493960,
			"isDeleted": false,
			"id": "LmuNv6oHzuFi_5TAZCOS1",
			"fillStyle": "solid",
			"strokeWidth": 1,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": 895.1605754960075,
			"y": 528.2367207752552,
			"strokeColor": "#000000",
			"backgroundColor": "#ced4da",
			"width": 71.66451803756424,
			"height": 92.4944378166419,
			"seed": 95209080,
			"groupIds": [
				"z0zMkhdwaZ0ynJDrtLFhR",
				"UN-69qqPKorbRQe09iRCz",
				"wH5gPqbCPVpccPFRtHFid",
				"3D7FOAwyMVuxnZrYz7c2H"
			],
			"frameId": null,
			"roundness": {
				"type": 2
			},
			"boundElements": null,
			"updated": 1711590984704,
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
					0.23631277756161562,
					69.90679477501719
				],
				[
					0.011058883236775303,
					77.86537979260234
				],
				[
					3.690881175524461,
					81.30418596549401
				],
				[
					16.505678697187165,
					84.21452947378963
				],
				[
					38.166316523905,
					85.12076696651043
				],
				[
					58.86162358869831,
					83.67382606057318
				],
				[
					69.85719260843815,
					80.2134930539004
				],
				[
					71.40796883026277,
					77.29639602912391
				],
				[
					71.62576973675768,
					70.88899726829273
				],
				[
					71.45482135084606,
					5.864789891179346
				],
				[
					71.06944881668004,
					-0.27879963213419856
				],
				[
					66.4678637859641,
					-3.712492230559498
				],
				[
					56.77790772977523,
					-5.70110529183138
				],
				[
					34.69580711193442,
					-7.373670850131469
				],
				[
					16.99156283916344,
					-6.376316241616809
				],
				[
					3.0672949545182333,
					-2.9934111019973204
				],
				[
					-0.038748300806571497,
					-0.04200446053826079
				],
				[
					0,
					0
				]
			]
		},
		{
			"type": "ellipse",
			"version": 7505,
			"versionNonce": 485366792,
			"isDeleted": false,
			"id": "idga6g4F5esK4ynY1LDAe",
			"fillStyle": "solid",
			"strokeWidth": 1,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": 895.3110805419207,
			"y": 521.0285505122274,
			"strokeColor": "#000000",
			"backgroundColor": "#fff",
			"width": 71.20485008239825,
			"height": 14.40064523308222,
			"seed": 440219512,
			"groupIds": [
				"z0zMkhdwaZ0ynJDrtLFhR",
				"UN-69qqPKorbRQe09iRCz",
				"wH5gPqbCPVpccPFRtHFid",
				"3D7FOAwyMVuxnZrYz7c2H"
			],
			"frameId": null,
			"roundness": null,
			"boundElements": null,
			"updated": 1711590984704,
			"link": null,
			"locked": false
		},
		{
			"type": "diamond",
			"version": 1770,
			"versionNonce": 1742560008,
			"isDeleted": false,
			"id": "PbMa6q3jBTaus63cU_CqJ",
			"fillStyle": "solid",
			"strokeWidth": 1,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": 937.6374900155666,
			"y": 542.7189637949871,
			"strokeColor": "#000000",
			"backgroundColor": "#868e96",
			"width": 22.14493603658657,
			"height": 25.74992562393783,
			"seed": 93816952,
			"groupIds": [
				"UN-69qqPKorbRQe09iRCz",
				"wH5gPqbCPVpccPFRtHFid",
				"3D7FOAwyMVuxnZrYz7c2H"
			],
			"frameId": null,
			"roundness": null,
			"boundElements": null,
			"updated": 1711590984704,
			"link": null,
			"locked": false
		},
		{
			"type": "ellipse",
			"version": 1977,
			"versionNonce": 814529032,
			"isDeleted": false,
			"id": "7heRWnV3cl1cwlMKt_c47",
			"fillStyle": "solid",
			"strokeWidth": 1,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": 925.2775257160741,
			"y": 581.858850743373,
			"strokeColor": "#000000",
			"backgroundColor": "#868e96",
			"width": 23.68993157402284,
			"height": 22.659934549065266,
			"seed": 327137656,
			"groupIds": [
				"UN-69qqPKorbRQe09iRCz",
				"wH5gPqbCPVpccPFRtHFid",
				"3D7FOAwyMVuxnZrYz7c2H"
			],
			"frameId": null,
			"roundness": null,
			"boundElements": null,
			"updated": 1711590984704,
			"link": null,
			"locked": false
		},
		{
			"type": "line",
			"version": 3309,
			"versionNonce": 167262472,
			"isDeleted": false,
			"id": "KI3r4zKC64Xmn7EgTUs3T",
			"fillStyle": "solid",
			"strokeWidth": 1,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": 914.4205982298714,
			"y": 556.0205006622163,
			"strokeColor": "#000000",
			"backgroundColor": "#868e96",
			"width": 21.51796361426944,
			"height": 19.662074531243835,
			"seed": 2000276088,
			"groupIds": [
				"UN-69qqPKorbRQe09iRCz",
				"wH5gPqbCPVpccPFRtHFid",
				"3D7FOAwyMVuxnZrYz7c2H"
			],
			"frameId": null,
			"roundness": null,
			"boundElements": null,
			"updated": 1711590984704,
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
					10.48483163908686,
					19.662074531243835
				],
				[
					-11.03313197518258,
					19.42132297980718
				],
				[
					0,
					0
				]
			]
		},
		{
			"type": "line",
			"version": 6732,
			"versionNonce": 339449464,
			"isDeleted": false,
			"id": "cVhgvMIdLpG9Pm3-0ItSi",
			"fillStyle": "solid",
			"strokeWidth": 1,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": 1017.3952058857767,
			"y": 528.4396934206135,
			"strokeColor": "#000000",
			"backgroundColor": "#ced4da",
			"width": 71.66451803756424,
			"height": 92.4944378166419,
			"seed": 812074616,
			"groupIds": [
				"a0cJrcJwySofwCwDNsuJB",
				"uDga2qOv0c5yySsfv0Gv4",
				"TkNjc9CCMXZpLQHh-gdnx",
				"ACAjyYkDoXldUgvJMAOFr"
			],
			"frameId": null,
			"roundness": {
				"type": 2
			},
			"boundElements": null,
			"updated": 1711591147148,
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
					0.23631277756161562,
					69.90679477501719
				],
				[
					0.011058883236775303,
					77.86537979260234
				],
				[
					3.690881175524461,
					81.30418596549401
				],
				[
					16.505678697187165,
					84.21452947378963
				],
				[
					38.166316523905,
					85.12076696651043
				],
				[
					58.86162358869831,
					83.67382606057318
				],
				[
					69.85719260843815,
					80.2134930539004
				],
				[
					71.40796883026277,
					77.29639602912391
				],
				[
					71.62576973675768,
					70.88899726829273
				],
				[
					71.45482135084606,
					5.864789891179346
				],
				[
					71.06944881668004,
					-0.27879963213419856
				],
				[
					66.4678637859641,
					-3.712492230559498
				],
				[
					56.77790772977523,
					-5.70110529183138
				],
				[
					34.69580711193442,
					-7.373670850131469
				],
				[
					16.99156283916344,
					-6.376316241616809
				],
				[
					3.0672949545182333,
					-2.9934111019973204
				],
				[
					-0.038748300806571497,
					-0.04200446053826079
				],
				[
					0,
					0
				]
			]
		},
		{
			"type": "ellipse",
			"version": 7560,
			"versionNonce": 242354040,
			"isDeleted": false,
			"id": "RaA4sCO4mMAMeSE83Te-Y",
			"fillStyle": "solid",
			"strokeWidth": 1,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": 1017.5457109316899,
			"y": 521.2315231575857,
			"strokeColor": "#000000",
			"backgroundColor": "#fff",
			"width": 71.20485008239825,
			"height": 14.40064523308222,
			"seed": 1634761992,
			"groupIds": [
				"a0cJrcJwySofwCwDNsuJB",
				"uDga2qOv0c5yySsfv0Gv4",
				"TkNjc9CCMXZpLQHh-gdnx",
				"ACAjyYkDoXldUgvJMAOFr"
			],
			"frameId": null,
			"roundness": null,
			"boundElements": null,
			"updated": 1711591147148,
			"link": null,
			"locked": false
		},
		{
			"type": "diamond",
			"version": 1825,
			"versionNonce": 984766584,
			"isDeleted": false,
			"id": "3MFVJtRC5eaF2Bbmg7mGj",
			"fillStyle": "solid",
			"strokeWidth": 1,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": 1059.8721204053359,
			"y": 542.9219364403453,
			"strokeColor": "#000000",
			"backgroundColor": "#868e96",
			"width": 22.14493603658657,
			"height": 25.74992562393783,
			"seed": 161986424,
			"groupIds": [
				"uDga2qOv0c5yySsfv0Gv4",
				"TkNjc9CCMXZpLQHh-gdnx",
				"ACAjyYkDoXldUgvJMAOFr"
			],
			"frameId": null,
			"roundness": null,
			"boundElements": null,
			"updated": 1711591147148,
			"link": null,
			"locked": false
		},
		{
			"type": "ellipse",
			"version": 2032,
			"versionNonce": 2092992888,
			"isDeleted": false,
			"id": "yAfsnw0kFlZjhmZ1NAO-J",
			"fillStyle": "solid",
			"strokeWidth": 1,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": 1047.5121561058434,
			"y": 582.0618233887312,
			"strokeColor": "#000000",
			"backgroundColor": "#868e96",
			"width": 23.68993157402284,
			"height": 22.659934549065266,
			"seed": 258710536,
			"groupIds": [
				"uDga2qOv0c5yySsfv0Gv4",
				"TkNjc9CCMXZpLQHh-gdnx",
				"ACAjyYkDoXldUgvJMAOFr"
			],
			"frameId": null,
			"roundness": null,
			"boundElements": null,
			"updated": 1711591147148,
			"link": null,
			"locked": false
		},
		{
			"type": "line",
			"version": 3364,
			"versionNonce": 534813304,
			"isDeleted": false,
			"id": "FRXguHgFvhsShYEhIATOP",
			"fillStyle": "solid",
			"strokeWidth": 1,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": 1036.6552286196406,
			"y": 556.2234733075745,
			"strokeColor": "#000000",
			"backgroundColor": "#868e96",
			"width": 21.51796361426944,
			"height": 19.662074531243835,
			"seed": 598870136,
			"groupIds": [
				"uDga2qOv0c5yySsfv0Gv4",
				"TkNjc9CCMXZpLQHh-gdnx",
				"ACAjyYkDoXldUgvJMAOFr"
			],
			"frameId": null,
			"roundness": null,
			"boundElements": null,
			"updated": 1711591147148,
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
					10.48483163908686,
					19.662074531243835
				],
				[
					-11.03313197518258,
					19.42132297980718
				],
				[
					0,
					0
				]
			]
		},
		{
			"id": "90Jm58sKkmgEgnFMewqoO",
			"type": "arrow",
			"x": 698.6357349555615,
			"y": 570.1406858430564,
			"width": 174.8888547005089,
			"height": 11.89825003753458,
			"angle": 0,
			"strokeColor": "#1e1e1e",
			"backgroundColor": "transparent",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"groupIds": [],
			"frameId": null,
			"roundness": {
				"type": 2
			},
			"seed": 1296344952,
			"version": 195,
			"versionNonce": 1949905784,
			"isDeleted": false,
			"boundElements": [
				{
					"type": "text",
					"id": "sUYQjlIY"
				}
			],
			"updated": 1711590725303,
			"link": null,
			"locked": false,
			"points": [
				[
					0,
					0
				],
				[
					174.8888547005089,
					11.89825003753458
				]
			],
			"lastCommittedPoint": [
				170.39049243516172,
				0
			],
			"startBinding": {
				"elementId": "CnSQZuPZVa17A40oRGiea",
				"focus": -0.2623853899104163,
				"gap": 17.774722473356178
			},
			"endBinding": null,
			"startArrowhead": null,
			"endArrowhead": "arrow"
		},
		{
			"id": "sUYQjlIY",
			"type": "text",
			"x": 726.4972254653981,
			"y": 560.1406858430564,
			"width": 85.55195617675781,
			"height": 20,
			"angle": 0,
			"strokeColor": "#1e1e1e",
			"backgroundColor": "transparent",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"seed": 1644222984,
			"version": 34,
			"versionNonce": 212962424,
			"isDeleted": false,
			"boundElements": null,
			"updated": 1711589268080,
			"link": null,
			"locked": false,
			"text": "save image",
			"rawText": "save image",
			"fontSize": 16,
			"fontFamily": 1,
			"textAlign": "center",
			"verticalAlign": "middle",
			"baseline": 14,
			"containerId": "90Jm58sKkmgEgnFMewqoO",
			"originalText": "save image",
			"lineHeight": 1.25
		},
		{
			"id": "Mmz7Xppu",
			"type": "text",
			"x": 187.58691286194843,
			"y": 981.3924344397448,
			"width": 351.6477966308594,
			"height": 100,
			"angle": 0,
			"strokeColor": "#1e1e1e",
			"backgroundColor": "transparent",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"seed": 1407504136,
			"version": 477,
			"versionNonce": 1535636600,
			"isDeleted": false,
			"boundElements": null,
			"updated": 1711591652736,
			"link": null,
			"locked": false,
			"text": "Possible extensions:\n\n- Device could do compression before sending\n  photo to the server.\n- More details on how to handle sharding.",
			"rawText": "Possible extensions:\n\n- Device could do compression before sending\n  photo to the server.\n- More details on how to handle sharding.",
			"fontSize": 16,
			"fontFamily": 1,
			"textAlign": "left",
			"verticalAlign": "top",
			"baseline": 94,
			"containerId": null,
			"originalText": "Possible extensions:\n\n- Device could do compression before sending\n  photo to the server.\n- More details on how to handle sharding.",
			"lineHeight": 1.25
		},
		{
			"type": "rectangle",
			"version": 590,
			"versionNonce": 1418366584,
			"isDeleted": false,
			"id": "uyk4xi8psVylwaoUV_mGy",
			"fillStyle": "hachure",
			"strokeWidth": 1,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": 684.6667424555009,
			"y": 138.34403573964846,
			"strokeColor": "#000000",
			"backgroundColor": "transparent",
			"width": 270.12152099609375,
			"height": 149.41595458984375,
			"seed": 1786727432,
			"groupIds": [
				"PhGwjslzSYdQn5SsPQ_Lv"
			],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1711591120190,
			"link": null,
			"locked": false
		},
		{
			"type": "line",
			"version": 529,
			"versionNonce": 1512177528,
			"isDeleted": false,
			"id": "uDV209Hbv2GMD02hh2Eou",
			"fillStyle": "hachure",
			"strokeWidth": 1,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": 687.0920964594071,
			"y": 176.90064584707034,
			"strokeColor": "#000000",
			"backgroundColor": "transparent",
			"width": 269.38385009765625,
			"height": 1.72381591796875,
			"seed": 1271433992,
			"groupIds": [
				"PhGwjslzSYdQn5SsPQ_Lv"
			],
			"frameId": null,
			"roundness": {
				"type": 2
			},
			"boundElements": [],
			"updated": 1711591120190,
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
			"id": "eaUTk4w5",
			"type": "text",
			"x": 694.9021767137036,
			"y": 147.39764566809612,
			"width": 43.16795349121094,
			"height": 20,
			"angle": 0,
			"strokeColor": "#1e1e1e",
			"backgroundColor": "transparent",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"groupIds": [
				"PhGwjslzSYdQn5SsPQ_Lv"
			],
			"frameId": null,
			"roundness": null,
			"seed": 115270008,
			"version": 414,
			"versionNonce": 2107854968,
			"isDeleted": false,
			"boundElements": null,
			"updated": 1711591120190,
			"link": null,
			"locked": false,
			"text": "posts",
			"rawText": "posts",
			"fontSize": 16,
			"fontFamily": 1,
			"textAlign": "left",
			"verticalAlign": "top",
			"baseline": 14,
			"containerId": null,
			"originalText": "posts",
			"lineHeight": 1.25
		},
		{
			"id": "SMVgfOhz",
			"type": "text",
			"x": 692.2095757629176,
			"y": 185.56686636061937,
			"width": 183.8718719482422,
			"height": 120,
			"angle": 0,
			"strokeColor": "#1e1e1e",
			"backgroundColor": "transparent",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"groupIds": [
				"PhGwjslzSYdQn5SsPQ_Lv"
			],
			"frameId": null,
			"roundness": null,
			"seed": 1924386568,
			"version": 524,
			"versionNonce": 651329912,
			"isDeleted": false,
			"boundElements": null,
			"updated": 1711591120190,
			"link": null,
			"locked": false,
			"text": "image_link: url\nuser_id: ID\ncreated_at: timestamp\ndescription: str\n\n",
			"rawText": "image_link: url\nuser_id: ID\ncreated_at: timestamp\ndescription: str\n\n",
			"fontSize": 16,
			"fontFamily": 1,
			"textAlign": "left",
			"verticalAlign": "top",
			"baseline": 114,
			"containerId": null,
			"originalText": "image_link: url\nuser_id: ID\ncreated_at: timestamp\ndescription: str\n\n",
			"lineHeight": 1.25
		},
		{
			"type": "line",
			"version": 6635,
			"versionNonce": 1905506824,
			"isDeleted": false,
			"id": "qZqmiTVDxcaYl07QqYpjf",
			"fillStyle": "solid",
			"strokeWidth": 1,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": 686.4178547717222,
			"y": 319.1123725900759,
			"strokeColor": "#000000",
			"backgroundColor": "#ced4da",
			"width": 75.01121630306868,
			"height": 96.81388324216654,
			"seed": 1971739400,
			"groupIds": [
				"DaxmKveeUU3GtQa77BqPW",
				"bzRkbAMIIAcNw1Rw9jam-",
				"Dn97xOGkpLSacJ3kkMUdS"
			],
			"frameId": null,
			"roundness": {
				"type": 2
			},
			"boundElements": [],
			"updated": 1711590300204,
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
					0.24734846976242794,
					73.1714082159101
				],
				[
					0.011575327725072006,
					81.50165529728328
				],
				[
					3.8632435379119165,
					85.10105205208878
				],
				[
					17.276485894102954,
					88.14730719194147
				],
				[
					39.948665011120255,
					89.0958655364321
				],
				[
					61.61043288740646,
					87.58135319133916
				],
				[
					73.11948965218787,
					83.95942431004657
				],
				[
					74.74268637210398,
					80.90610026776591
				],
				[
					74.9706584753909,
					74.19947908967055
				],
				[
					74.79172688269483,
					6.138672737165569
				],
				[
					74.38835763792527,
					-0.2918194398554754
				],
				[
					69.57188081608908,
					-3.885863818744892
				],
				[
					59.42940850758881,
					-5.967344146345569
				],
				[
					36.31608449133351,
					-7.7180177057344235
				],
				[
					17.785060590062127,
					-6.674087120295436
				],
				[
					3.210536142559118,
					-3.1332019499277424
				],
				[
					-0.04055782767777212,
					-0.04396604849106378
				],
				[
					0,
					0
				]
			]
		},
		{
			"type": "ellipse",
			"version": 7358,
			"versionNonce": 867915528,
			"isDeleted": false,
			"id": "l8QVFBoh-GGt0TAAMsREI",
			"fillStyle": "solid",
			"strokeWidth": 1,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": 686.6837873624062,
			"y": 310.35940443404786,
			"strokeColor": "#000000",
			"backgroundColor": "#fff",
			"width": 74.53008207714048,
			"height": 15.073148387271289,
			"seed": 555072008,
			"groupIds": [
				"DaxmKveeUU3GtQa77BqPW",
				"bzRkbAMIIAcNw1Rw9jam-",
				"Dn97xOGkpLSacJ3kkMUdS"
			],
			"frameId": null,
			"roundness": null,
			"boundElements": [
				{
					"id": "CeiVOZ_eCH2mjH70pPJ9M",
					"type": "arrow"
				}
			],
			"updated": 1711590464825,
			"link": null,
			"locked": false
		},
		{
			"type": "line",
			"version": 6744,
			"versionNonce": 249794056,
			"isDeleted": false,
			"id": "Yqrr8SwMxHLTywFJRsIjJ",
			"fillStyle": "solid",
			"strokeWidth": 1,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": 679.5446840794962,
			"y": 308.071636302722,
			"strokeColor": "#000000",
			"backgroundColor": "#ced4da",
			"width": 75.01121630306868,
			"height": 96.81388324216654,
			"seed": 1347437944,
			"groupIds": [
				"ng_IRzH0s2IRgoysKBxie",
				"Dz6hnuXyGSYcFKDPYlGaw",
				"XeZrcKR0MJMBZxoM1uuj7"
			],
			"frameId": null,
			"roundness": {
				"type": 2
			},
			"boundElements": null,
			"updated": 1711591118261,
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
					0.24734846976242794,
					73.1714082159101
				],
				[
					0.011575327725072006,
					81.50165529728328
				],
				[
					3.8632435379119165,
					85.10105205208878
				],
				[
					17.276485894102954,
					88.14730719194147
				],
				[
					39.948665011120255,
					89.0958655364321
				],
				[
					61.61043288740646,
					87.58135319133916
				],
				[
					73.11948965218787,
					83.95942431004657
				],
				[
					74.74268637210398,
					80.90610026776591
				],
				[
					74.9706584753909,
					74.19947908967055
				],
				[
					74.79172688269483,
					6.138672737165569
				],
				[
					74.38835763792527,
					-0.2918194398554754
				],
				[
					69.57188081608908,
					-3.885863818744892
				],
				[
					59.42940850758881,
					-5.967344146345569
				],
				[
					36.31608449133351,
					-7.7180177057344235
				],
				[
					17.785060590062127,
					-6.674087120295436
				],
				[
					3.210536142559118,
					-3.1332019499277424
				],
				[
					-0.04055782767777212,
					-0.04396604849106378
				],
				[
					0,
					0
				]
			]
		},
		{
			"type": "ellipse",
			"version": 7468,
			"versionNonce": 508857608,
			"isDeleted": false,
			"id": "8NAClcOLd6jYbRqphFtsf",
			"fillStyle": "solid",
			"strokeWidth": 1,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": 679.8106166701801,
			"y": 299.318668146694,
			"strokeColor": "#000000",
			"backgroundColor": "#fff",
			"width": 74.53008207714048,
			"height": 15.073148387271289,
			"seed": 1339747848,
			"groupIds": [
				"ng_IRzH0s2IRgoysKBxie",
				"Dz6hnuXyGSYcFKDPYlGaw",
				"XeZrcKR0MJMBZxoM1uuj7"
			],
			"frameId": null,
			"roundness": null,
			"boundElements": [
				{
					"id": "CeiVOZ_eCH2mjH70pPJ9M",
					"type": "arrow"
				}
			],
			"updated": 1711591118261,
			"link": null,
			"locked": false
		},
		{
			"id": "pAgjnBHfyGmYu6uyJq2Ke",
			"type": "arrow",
			"x": 683.3700865268339,
			"y": 517.052132772337,
			"width": 37.23570685280288,
			"height": 102.23789253890129,
			"angle": 0,
			"strokeColor": "#1e1e1e",
			"backgroundColor": "transparent",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"groupIds": [],
			"frameId": null,
			"roundness": {
				"type": 2
			},
			"seed": 447532152,
			"version": 309,
			"versionNonce": 936628088,
			"isDeleted": false,
			"boundElements": [
				{
					"type": "text",
					"id": "xiFuli21"
				}
			],
			"updated": 1711590642500,
			"link": null,
			"locked": false,
			"points": [
				[
					0,
					0
				],
				[
					37.23570685280288,
					-102.23789253890129
				]
			],
			"lastCommittedPoint": [
				170.0122934383503,
				-93.79719183466716
			],
			"startBinding": {
				"elementId": "NE7r0GWkhpC_qgDFN63wO",
				"focus": 0.6391249563158775,
				"gap": 13.372420698224573
			},
			"endBinding": null,
			"startArrowhead": null,
			"endArrowhead": "arrow"
		},
		{
			"id": "xiFuli21",
			"type": "text",
			"x": 707.8288213405762,
			"y": 457.94710980728274,
			"width": 122.5599365234375,
			"height": 20,
			"angle": 0,
			"strokeColor": "#1e1e1e",
			"backgroundColor": "transparent",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"seed": 1943950968,
			"version": 14,
			"versionNonce": 357662472,
			"isDeleted": false,
			"boundElements": null,
			"updated": 1711589611320,
			"link": null,
			"locked": false,
			"text": "save metadata",
			"rawText": "save metadata",
			"fontSize": 16,
			"fontFamily": 1,
			"textAlign": "center",
			"verticalAlign": "middle",
			"baseline": 14,
			"containerId": "pAgjnBHfyGmYu6uyJq2Ke",
			"originalText": "save metadata",
			"lineHeight": 1.25
		},
		{
			"id": "zz4n1wx0QcbUHZHH6NdMp",
			"type": "arrow",
			"x": 228.13918878585764,
			"y": 591.0197331581808,
			"width": 203.09640873560835,
			"height": 0,
			"angle": 0,
			"strokeColor": "#1971c2",
			"backgroundColor": "transparent",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"groupIds": [],
			"frameId": null,
			"roundness": {
				"type": 2
			},
			"seed": 1695608,
			"version": 323,
			"versionNonce": 1438157320,
			"isDeleted": false,
			"boundElements": [
				{
					"type": "text",
					"id": "P81NgQkP"
				}
			],
			"updated": 1711590632156,
			"link": null,
			"locked": false,
			"points": [
				[
					0,
					0
				],
				[
					203.09640873560835,
					0
				]
			],
			"lastCommittedPoint": [
				203.09640873560835,
				0
			],
			"startBinding": {
				"elementId": "Fp4GUsYjbYsT-oeTxBm9a",
				"focus": 0.361982347292459,
				"gap": 16.34264435439951
			},
			"endBinding": {
				"elementId": "ql6LG2EuU-F-mYLltKJvg",
				"focus": -0.2720084265853302,
				"gap": 10.071935158405438
			},
			"startArrowhead": null,
			"endArrowhead": "arrow"
		},
		{
			"id": "P81NgQkP",
			"type": "text",
			"x": 417.531662854007,
			"y": 581.0197331581808,
			"width": 85.07192993164062,
			"height": 20,
			"angle": 0,
			"strokeColor": "#1971c2",
			"backgroundColor": "transparent",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"seed": 662964856,
			"version": 16,
			"versionNonce": 271063928,
			"isDeleted": false,
			"boundElements": null,
			"updated": 1711589697111,
			"link": null,
			"locked": false,
			"text": "follow user",
			"rawText": "follow user",
			"fontSize": 16,
			"fontFamily": 1,
			"textAlign": "center",
			"verticalAlign": "middle",
			"baseline": 14,
			"containerId": "zz4n1wx0QcbUHZHH6NdMp",
			"originalText": "follow user",
			"lineHeight": 1.25
		},
		{
			"type": "text",
			"version": 1272,
			"versionNonce": 1518458744,
			"isDeleted": false,
			"id": "zGOEJ1HC",
			"fillStyle": "solid",
			"strokeWidth": 1,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": 947.8382715616112,
			"y": 437.55764093002347,
			"strokeColor": "#000000",
			"backgroundColor": "transparent",
			"width": 87.99256474002232,
			"height": 24.242849469189828,
			"seed": 852056072,
			"groupIds": [
				"V_sxEaqxjQ2fKyFo5NK5s"
			],
			"frameId": null,
			"roundness": null,
			"boundElements": [
				{
					"id": "t5cnS97ON8dGAg6wFa1nb",
					"type": "arrow"
				}
			],
			"updated": 1711590295842,
			"link": null,
			"locked": false,
			"fontSize": 17.957666273473947,
			"fontFamily": 1,
			"text": "Graph DB",
			"rawText": "",
			"textAlign": "center",
			"verticalAlign": "top",
			"containerId": null,
			"originalText": "Graph DB",
			"lineHeight": 1.3499999999999999,
			"baseline": 16
		},
		{
			"type": "line",
			"version": 6129,
			"versionNonce": 1245866616,
			"isDeleted": false,
			"id": "_yJ9dJXsc1hNK69841xbf",
			"fillStyle": "solid",
			"strokeWidth": 1,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": 953.5011837917547,
			"y": 344.7805692669686,
			"strokeColor": "#000000",
			"backgroundColor": "#ced4da",
			"width": 76.12508643688668,
			"height": 98.25150948524306,
			"seed": 384898824,
			"groupIds": [
				"J-egdMZUafFszw2pBu3hH",
				"GLEYAT5jctL7TuLMGha2m",
				"V_sxEaqxjQ2fKyFo5NK5s"
			],
			"frameId": null,
			"roundness": {
				"type": 2
			},
			"boundElements": [],
			"updated": 1711590295842,
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
					0.25102144144176597,
					74.25795833838522
				],
				[
					0.011747214177226184,
					82.71190443290023
				],
				[
					3.92061031329066,
					86.36475000166352
				],
				[
					17.53303101632861,
					89.45624014485985
				],
				[
					40.54187796026104,
					90.4188839936548
				],
				[
					62.52530968193274,
					88.88188207764664
				],
				[
					74.2052688161266,
					85.20616979426389
				],
				[
					75.85256900265384,
					82.10750577981393
				],
				[
					76.0839263505712,
					75.30129542829506
				],
				[
					75.90233773447324,
					6.229828227773573
				],
				[
					75.49297870608481,
					-0.2961527779153492
				],
				[
					70.60498018460845,
					-3.9435664912931654
				],
				[
					60.31189844002253,
					-6.055955513423964
				],
				[
					36.85535586814561,
					-7.832625491588246
				],
				[
					18.049157731739815,
					-6.773193183097575
				],
				[
					3.258210617110904,
					-3.1797280595850514
				],
				[
					-0.04116008631547069,
					-0.04461891709832333
				],
				[
					0,
					0
				]
			]
		},
		{
			"type": "ellipse",
			"version": 6898,
			"versionNonce": 2081057544,
			"isDeleted": false,
			"id": "4b9u6XmI0CNhnE31Y3n1w",
			"fillStyle": "solid",
			"strokeWidth": 1,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": 952.9291619612977,
			"y": 335.91139204397064,
			"strokeColor": "#000000",
			"backgroundColor": "#fff",
			"width": 75.63680766550185,
			"height": 15.296975311278919,
			"seed": 1036580360,
			"groupIds": [
				"J-egdMZUafFszw2pBu3hH",
				"GLEYAT5jctL7TuLMGha2m",
				"V_sxEaqxjQ2fKyFo5NK5s"
			],
			"frameId": null,
			"roundness": null,
			"boundElements": [
				{
					"id": "uzvve57SlzjrBxqeRUTQw",
					"type": "arrow"
				}
			],
			"updated": 1711590512705,
			"link": null,
			"locked": false
		},
		{
			"type": "ellipse",
			"version": 1395,
			"versionNonce": 1410608248,
			"isDeleted": false,
			"id": "lDBd0HV4Jr9eDVHGjnGWr",
			"fillStyle": "solid",
			"strokeWidth": 1,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": 987.1765491556255,
			"y": 359.12532385354933,
			"strokeColor": "#000000",
			"backgroundColor": "#868e96",
			"width": 9.607022561321903,
			"height": 9.607022561321903,
			"seed": 474805512,
			"groupIds": [
				"dZT5GxXsEGO_VJUMoz8Mx",
				"GLEYAT5jctL7TuLMGha2m",
				"V_sxEaqxjQ2fKyFo5NK5s"
			],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1711590295842,
			"link": null,
			"locked": false
		},
		{
			"type": "ellipse",
			"version": 1438,
			"versionNonce": 851959160,
			"isDeleted": false,
			"id": "XDnEfMulVzscsfn39iPeP",
			"fillStyle": "solid",
			"strokeWidth": 1,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": 962.5324478026721,
			"y": 377.5039757099917,
			"strokeColor": "#000000",
			"backgroundColor": "#868e96",
			"width": 9.607022561321903,
			"height": 9.607022561321903,
			"seed": 670635016,
			"groupIds": [
				"dZT5GxXsEGO_VJUMoz8Mx",
				"GLEYAT5jctL7TuLMGha2m",
				"V_sxEaqxjQ2fKyFo5NK5s"
			],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1711590295842,
			"link": null,
			"locked": false
		},
		{
			"type": "ellipse",
			"version": 1436,
			"versionNonce": 1105030776,
			"isDeleted": false,
			"id": "PCJ9Pnh_il1IhbT8xQCj1",
			"fillStyle": "solid",
			"strokeWidth": 1,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": 1011.4029538754833,
			"y": 377.0862790768909,
			"strokeColor": "#000000",
			"backgroundColor": "#868e96",
			"width": 9.607022561321903,
			"height": 9.607022561321903,
			"seed": 1187599112,
			"groupIds": [
				"dZT5GxXsEGO_VJUMoz8Mx",
				"GLEYAT5jctL7TuLMGha2m",
				"V_sxEaqxjQ2fKyFo5NK5s"
			],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1711590295842,
			"link": null,
			"locked": false
		},
		{
			"type": "ellipse",
			"version": 1467,
			"versionNonce": 1511579512,
			"isDeleted": false,
			"id": "cSyGgJ5cvrB5ysiYRCsz_",
			"fillStyle": "solid",
			"strokeWidth": 1,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": 1003.0490212134648,
			"y": 406.32504339395723,
			"strokeColor": "#000000",
			"backgroundColor": "#868e96",
			"width": 9.607022561321903,
			"height": 9.607022561321903,
			"seed": 1060745736,
			"groupIds": [
				"dZT5GxXsEGO_VJUMoz8Mx",
				"GLEYAT5jctL7TuLMGha2m",
				"V_sxEaqxjQ2fKyFo5NK5s"
			],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1711590295842,
			"link": null,
			"locked": false
		},
		{
			"type": "ellipse",
			"version": 1485,
			"versionNonce": 465449080,
			"isDeleted": false,
			"id": "ck82V7tCXqOpIm19Rth_7",
			"fillStyle": "solid",
			"strokeWidth": 1,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": 971.5129254143428,
			"y": 406.5338917105073,
			"strokeColor": "#000000",
			"backgroundColor": "#868e96",
			"width": 9.607022561321903,
			"height": 9.607022561321903,
			"seed": 675688712,
			"groupIds": [
				"dZT5GxXsEGO_VJUMoz8Mx",
				"GLEYAT5jctL7TuLMGha2m",
				"V_sxEaqxjQ2fKyFo5NK5s"
			],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1711590295842,
			"link": null,
			"locked": false
		},
		{
			"type": "line",
			"version": 1425,
			"versionNonce": 2123456888,
			"isDeleted": false,
			"id": "xjkeOLCF0p0pos8hkbJzZ",
			"fillStyle": "hachure",
			"strokeWidth": 1,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": 996.2824580103531,
			"y": 365.6611392072754,
			"strokeColor": "#000000",
			"backgroundColor": "#fa5252",
			"width": 16.776635630551436,
			"height": 12.433771197841677,
			"seed": 1500172296,
			"groupIds": [
				"dZT5GxXsEGO_VJUMoz8Mx",
				"GLEYAT5jctL7TuLMGha2m",
				"V_sxEaqxjQ2fKyFo5NK5s"
			],
			"frameId": null,
			"roundness": {
				"type": 2
			},
			"boundElements": [],
			"updated": 1711590295842,
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
					16.776635630551436,
					12.433771197841677
				]
			]
		},
		{
			"type": "line",
			"version": 1433,
			"versionNonce": 1641443960,
			"isDeleted": false,
			"id": "2POhNbeZZp9jGK-ipV9hg",
			"fillStyle": "hachure",
			"strokeWidth": 1,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": 1017.1965964173899,
			"y": 386.22853130064715,
			"strokeColor": "#000000",
			"backgroundColor": "#fa5252",
			"width": 6.292481153178085,
			"height": 19.736085416824245,
			"seed": 1520668424,
			"groupIds": [
				"dZT5GxXsEGO_VJUMoz8Mx",
				"GLEYAT5jctL7TuLMGha2m",
				"V_sxEaqxjQ2fKyFo5NK5s"
			],
			"frameId": null,
			"roundness": {
				"type": 2
			},
			"boundElements": [],
			"updated": 1711590295842,
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
					-6.292481153178085,
					19.736085416824245
				]
			]
		},
		{
			"type": "line",
			"version": 1434,
			"versionNonce": 475095928,
			"isDeleted": false,
			"id": "n8k37sTtrJjCb1KJrk2Lr",
			"fillStyle": "hachure",
			"strokeWidth": 1,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": 986.6517846085044,
			"y": 366.4904302048779,
			"strokeColor": "#000000",
			"backgroundColor": "#fa5252",
			"width": 17.61027875506922,
			"height": 12.156617537245793,
			"seed": 1416392200,
			"groupIds": [
				"dZT5GxXsEGO_VJUMoz8Mx",
				"GLEYAT5jctL7TuLMGha2m",
				"V_sxEaqxjQ2fKyFo5NK5s"
			],
			"frameId": null,
			"roundness": {
				"type": 2
			},
			"boundElements": [],
			"updated": 1711590295842,
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
					-17.61027875506922,
					12.156617537245793
				]
			]
		},
		{
			"type": "line",
			"version": 1413,
			"versionNonce": 205927544,
			"isDeleted": false,
			"id": "lOa8q8yoCk1YbOAM45U01",
			"fillStyle": "hachure",
			"strokeWidth": 1,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": 968.2158317311498,
			"y": 386.455378945502,
			"strokeColor": "#000000",
			"backgroundColor": "#fa5252",
			"width": 6.69823303698876,
			"height": 20.316107103575025,
			"seed": 2143382792,
			"groupIds": [
				"dZT5GxXsEGO_VJUMoz8Mx",
				"GLEYAT5jctL7TuLMGha2m",
				"V_sxEaqxjQ2fKyFo5NK5s"
			],
			"frameId": null,
			"roundness": {
				"type": 2
			},
			"boundElements": [],
			"updated": 1711590295842,
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
					6.69823303698876,
					20.316107103575025
				]
			]
		},
		{
			"type": "line",
			"version": 1411,
			"versionNonce": 662234488,
			"isDeleted": false,
			"id": "D13uwqAtRQtroKjctF-oF",
			"fillStyle": "hachure",
			"strokeWidth": 1,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": 981.3051826798267,
			"y": 412.2617284178484,
			"strokeColor": "#000000",
			"backgroundColor": "#fa5252",
			"width": 21.064985166516465,
			"height": 0.2721277017741712,
			"seed": 371100680,
			"groupIds": [
				"dZT5GxXsEGO_VJUMoz8Mx",
				"GLEYAT5jctL7TuLMGha2m",
				"V_sxEaqxjQ2fKyFo5NK5s"
			],
			"frameId": null,
			"roundness": {
				"type": 2
			},
			"boundElements": [],
			"updated": 1711590295842,
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
					21.064985166516465,
					-0.2721277017741712
				]
			]
		},
		{
			"type": "line",
			"version": 1430,
			"versionNonce": 187528824,
			"isDeleted": false,
			"id": "kuwseN-tNuKh6mLHZil0r",
			"fillStyle": "hachure",
			"strokeWidth": 1,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": 973.2444964272456,
			"y": 383.2426838782479,
			"strokeColor": "#000000",
			"backgroundColor": "#fa5252",
			"width": 39.041503046288675,
			"height": 0.1401686175701484,
			"seed": 1098894088,
			"groupIds": [
				"dZT5GxXsEGO_VJUMoz8Mx",
				"GLEYAT5jctL7TuLMGha2m",
				"V_sxEaqxjQ2fKyFo5NK5s"
			],
			"frameId": null,
			"roundness": {
				"type": 2
			},
			"boundElements": [],
			"updated": 1711590295842,
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
					39.041503046288675,
					0.1401686175701484
				]
			]
		},
		{
			"type": "line",
			"version": 1415,
			"versionNonce": 203941752,
			"isDeleted": false,
			"id": "-83RimXRQYoZs07BksEe_",
			"fillStyle": "hachure",
			"strokeWidth": 1,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": 991.7872169469308,
			"y": 368.9627818796028,
			"strokeColor": "#000000",
			"backgroundColor": "#fa5252",
			"width": 11.695505726826665,
			"height": 38.21924192873713,
			"seed": 207694344,
			"groupIds": [
				"dZT5GxXsEGO_VJUMoz8Mx",
				"GLEYAT5jctL7TuLMGha2m",
				"V_sxEaqxjQ2fKyFo5NK5s"
			],
			"frameId": null,
			"roundness": {
				"type": 2
			},
			"boundElements": [],
			"updated": 1711590295842,
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
					-11.695505726826665,
					38.21924192873713
				]
			]
		},
		{
			"type": "line",
			"version": 1399,
			"versionNonce": 1185691768,
			"isDeleted": false,
			"id": "dgtJbtgUfoPDDW3oHqBHo",
			"fillStyle": "hachure",
			"strokeWidth": 1,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": 993.9830114887366,
			"y": 368.94143689409685,
			"strokeColor": "#000000",
			"backgroundColor": "#fa5252",
			"width": 11.695505726826665,
			"height": 38.84578687838854,
			"seed": 1371449608,
			"groupIds": [
				"dZT5GxXsEGO_VJUMoz8Mx",
				"GLEYAT5jctL7TuLMGha2m",
				"V_sxEaqxjQ2fKyFo5NK5s"
			],
			"frameId": null,
			"roundness": {
				"type": 2
			},
			"boundElements": [],
			"updated": 1711590295842,
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
					11.695505726826665,
					38.84578687838854
				]
			]
		},
		{
			"type": "line",
			"version": 1374,
			"versionNonce": 780036472,
			"isDeleted": false,
			"id": "xmwXPTf2IVg4_pJlitX2f",
			"fillStyle": "hachure",
			"strokeWidth": 1,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": 980.3181995443567,
			"y": 407.8183259180182,
			"strokeColor": "#000000",
			"backgroundColor": "#fa5252",
			"width": 32.99803401497525,
			"height": 22.346769870900953,
			"seed": 756303880,
			"groupIds": [
				"dZT5GxXsEGO_VJUMoz8Mx",
				"GLEYAT5jctL7TuLMGha2m",
				"V_sxEaqxjQ2fKyFo5NK5s"
			],
			"frameId": null,
			"roundness": {
				"type": 2
			},
			"boundElements": [],
			"updated": 1711590295842,
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
					32.99803401497525,
					-22.346769870900953
				]
			]
		},
		{
			"type": "line",
			"version": 1408,
			"versionNonce": 518158968,
			"isDeleted": false,
			"id": "xOjzC_VnPWx9YrjCMvkXH",
			"fillStyle": "hachure",
			"strokeWidth": 1,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": 971.5186471097106,
			"y": 385.8067218936881,
			"strokeColor": "#000000",
			"backgroundColor": "#fa5252",
			"width": 33.41554690329783,
			"height": 22.023298789909873,
			"seed": 1784547080,
			"groupIds": [
				"dZT5GxXsEGO_VJUMoz8Mx",
				"GLEYAT5jctL7TuLMGha2m",
				"V_sxEaqxjQ2fKyFo5NK5s"
			],
			"frameId": null,
			"roundness": {
				"type": 2
			},
			"boundElements": [],
			"updated": 1711590295842,
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
					33.41554690329783,
					22.023298789909873
				]
			]
		},
		{
			"id": "t5cnS97ON8dGAg6wFa1nb",
			"type": "arrow",
			"x": 692.7767513935647,
			"y": 550.1121841554448,
			"width": 248.48528438409937,
			"height": 82.65499345409,
			"angle": 0,
			"strokeColor": "#1971c2",
			"backgroundColor": "transparent",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"groupIds": [],
			"frameId": null,
			"roundness": {
				"type": 2
			},
			"seed": 1521132808,
			"version": 1641,
			"versionNonce": 2014228088,
			"isDeleted": false,
			"boundElements": [
				{
					"type": "text",
					"id": "6w0NP3bW"
				}
			],
			"updated": 1711590655339,
			"link": null,
			"locked": false,
			"points": [
				[
					0,
					0
				],
				[
					248.48528438409937,
					-82.65499345409
				]
			],
			"lastCommittedPoint": [
				-33.207455078621024,
				-117.83739640809995
			],
			"startBinding": {
				"elementId": "CnSQZuPZVa17A40oRGiea",
				"focus": -0.13998496887536319,
				"gap": 11.915738911359426
			},
			"endBinding": {
				"elementId": "zGOEJ1HC",
				"focus": -0.03572700745722606,
				"gap": 6.576235783947141
			},
			"startArrowhead": null,
			"endArrowhead": "arrow"
		},
		{
			"id": "6w0NP3bW",
			"type": "text",
			"x": 547.5917731795746,
			"y": 419.324943017316,
			"width": 87.37593078613281,
			"height": 60,
			"angle": 0,
			"strokeColor": "#1971c2",
			"backgroundColor": "transparent",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"seed": 103311112,
			"version": 34,
			"versionNonce": 1555337080,
			"isDeleted": false,
			"boundElements": null,
			"updated": 1711589829861,
			"link": null,
			"locked": false,
			"text": "store\nfollower\nrelationship",
			"rawText": "store\nfollower\nrelationship",
			"fontSize": 16,
			"fontFamily": 1,
			"textAlign": "center",
			"verticalAlign": "middle",
			"baseline": 54,
			"containerId": "t5cnS97ON8dGAg6wFa1nb",
			"originalText": "store\nfollower\nrelationship",
			"lineHeight": 1.25
		},
		{
			"id": "3CPse1W4",
			"type": "text",
			"x": 1048.9014787042324,
			"y": 346.03490559042405,
			"width": 201.43988037109375,
			"height": 100,
			"angle": 0,
			"strokeColor": "#1e1e1e",
			"backgroundColor": "transparent",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"seed": 626138232,
			"version": 522,
			"versionNonce": 2064794744,
			"isDeleted": false,
			"boundElements": null,
			"updated": 1711590297622,
			"link": null,
			"locked": false,
			"text": "each user vertex\nhas indegrees from people\nthat are following them\nand outdegrees to people\nthat they follow.",
			"rawText": "each user vertex\nhas indegrees from people\nthat are following them\nand outdegrees to people\nthat they follow.",
			"fontSize": 16,
			"fontFamily": 1,
			"textAlign": "left",
			"verticalAlign": "top",
			"baseline": 94,
			"containerId": null,
			"originalText": "each user vertex\nhas indegrees from people\nthat are following them\nand outdegrees to people\nthat they follow.",
			"lineHeight": 1.25
		},
		{
			"id": "Jm4rtfW2NaUFjn6Ttuv19",
			"type": "rectangle",
			"x": 595.5615385062163,
			"y": 798.5665771469351,
			"width": 540.1662943730555,
			"height": 621.4988692598947,
			"angle": 0,
			"strokeColor": "#1e1e1e",
			"backgroundColor": "#eeeeee",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"groupIds": [
				"OoCmH0lHLqaYdKcrYUCdv"
			],
			"frameId": null,
			"roundness": null,
			"seed": 430256904,
			"version": 168,
			"versionNonce": 1403747192,
			"isDeleted": false,
			"boundElements": null,
			"updated": 1711591625410,
			"link": null,
			"locked": false
		},
		{
			"id": "0vnesiXj",
			"type": "text",
			"x": 620.2104156725848,
			"y": 818.556097181563,
			"width": 486.5276794433594,
			"height": 620,
			"angle": 0,
			"strokeColor": "#1e1e1e",
			"backgroundColor": "transparent",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"groupIds": [
				"OoCmH0lHLqaYdKcrYUCdv"
			],
			"frameId": null,
			"roundness": null,
			"seed": 1846587912,
			"version": 1848,
			"versionNonce": 10308728,
			"isDeleted": false,
			"boundElements": null,
			"updated": 1711591625410,
			"link": null,
			"locked": false,
			"text": "How to get the feed for a user?\n\n1. Get all the users that the user is following.\n2. Grab 50 most recent posts from all those users.\n3. Send list of posts back to the user.\n4. User can make requests to download actual\n   image files on a scrolling basis.\n\nHow to implement?\n\nPush:\n\n- Have a feed generation service that listens for\n  new images posted, and then performs the above\n  steps, writing the post_id to each follower's feed\n  in the cache.\n- This has the downside that for users with millions\n  of followers, millions of updates will need to be made\n  to our feed cache when they upload a photo.\n\nPull:\n\n- For celebrities, we can instead just have users pull\n  the new photo_ids when they go to view their feed.\n- This way, there isn't an immediate spike when a celebrity\n  posts a photo.\n- We could maintain a list/filter of accounts that should\n  use this \"pull\" paradigm instead of push; could be something\n  as simple as if they have >100K followers.\n\n",
			"rawText": "How to get the feed for a user?\n\n1. Get all the users that the user is following.\n2. Grab 50 most recent posts from all those users.\n3. Send list of posts back to the user.\n4. User can make requests to download actual\n   image files on a scrolling basis.\n\nHow to implement?\n\nPush:\n\n- Have a feed generation service that listens for\n  new images posted, and then performs the above\n  steps, writing the post_id to each follower's feed\n  in the cache.\n- This has the downside that for users with millions\n  of followers, millions of updates will need to be made\n  to our feed cache when they upload a photo.\n\nPull:\n\n- For celebrities, we can instead just have users pull\n  the new photo_ids when they go to view their feed.\n- This way, there isn't an immediate spike when a celebrity\n  posts a photo.\n- We could maintain a list/filter of accounts that should\n  use this \"pull\" paradigm instead of push; could be something\n  as simple as if they have >100K followers.\n\n",
			"fontSize": 16,
			"fontFamily": 1,
			"textAlign": "left",
			"verticalAlign": "top",
			"baseline": 614,
			"containerId": null,
			"originalText": "How to get the feed for a user?\n\n1. Get all the users that the user is following.\n2. Grab 50 most recent posts from all those users.\n3. Send list of posts back to the user.\n4. User can make requests to download actual\n   image files on a scrolling basis.\n\nHow to implement?\n\nPush:\n\n- Have a feed generation service that listens for\n  new images posted, and then performs the above\n  steps, writing the post_id to each follower's feed\n  in the cache.\n- This has the downside that for users with millions\n  of followers, millions of updates will need to be made\n  to our feed cache when they upload a photo.\n\nPull:\n\n- For celebrities, we can instead just have users pull\n  the new photo_ids when they go to view their feed.\n- This way, there isn't an immediate spike when a celebrity\n  posts a photo.\n- We could maintain a list/filter of accounts that should\n  use this \"pull\" paradigm instead of push; could be something\n  as simple as if they have >100K followers.\n\n",
			"lineHeight": 1.25
		},
		{
			"type": "rectangle",
			"version": 1614,
			"versionNonce": 222587256,
			"isDeleted": false,
			"id": "SK68WW9xyedBMNGyVuCDe",
			"fillStyle": "solid",
			"strokeWidth": 1,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": 250.8844938890495,
			"y": 29.292345790075473,
			"strokeColor": "#000000",
			"backgroundColor": "#eeeeee",
			"width": 97.35601825028085,
			"height": 98.60970239702232,
			"seed": 651284344,
			"groupIds": [
				"JO9GEsq-fRfgtnTTIFXwd"
			],
			"frameId": null,
			"roundness": null,
			"boundElements": [
				{
					"type": "text",
					"id": "5BRT2oe3"
				},
				{
					"id": "CeiVOZ_eCH2mjH70pPJ9M",
					"type": "arrow"
				},
				{
					"id": "uzvve57SlzjrBxqeRUTQw",
					"type": "arrow"
				},
				{
					"id": "w7IEkJFMpmZAgwUDktcy8",
					"type": "arrow"
				}
			],
			"updated": 1711590535203,
			"link": null,
			"locked": false
		},
		{
			"id": "5BRT2oe3",
			"type": "text",
			"x": 257.54651943264696,
			"y": 48.59719698858663,
			"width": 84.03196716308594,
			"height": 60,
			"angle": 0,
			"strokeColor": "#1e1e1e",
			"backgroundColor": "transparent",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"groupIds": [
				"JO9GEsq-fRfgtnTTIFXwd"
			],
			"frameId": null,
			"roundness": null,
			"seed": 351987464,
			"version": 266,
			"versionNonce": 471243640,
			"isDeleted": false,
			"boundElements": null,
			"updated": 1711590245666,
			"link": null,
			"locked": false,
			"text": "Feed\nGeneration\nService",
			"rawText": "Feed Generation\nService",
			"fontSize": 16,
			"fontFamily": 1,
			"textAlign": "center",
			"verticalAlign": "middle",
			"baseline": 54,
			"containerId": "SK68WW9xyedBMNGyVuCDe",
			"originalText": "Feed Generation\nService",
			"lineHeight": 1.25
		},
		{
			"type": "rectangle",
			"version": 1661,
			"versionNonce": 761984520,
			"isDeleted": false,
			"id": "AEWwLZQGGSSWESQ1z96_d",
			"fillStyle": "solid",
			"strokeWidth": 1,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": 241.1908302592817,
			"y": 14.316295334562312,
			"strokeColor": "#000000",
			"backgroundColor": "#eeeeee",
			"width": 97.35601825028085,
			"height": 98.60970239702232,
			"seed": 2029384312,
			"groupIds": [
				"Z1X4KnfgbIEnb87--WOIB"
			],
			"frameId": null,
			"roundness": null,
			"boundElements": [
				{
					"id": "CeiVOZ_eCH2mjH70pPJ9M",
					"type": "arrow"
				},
				{
					"id": "uzvve57SlzjrBxqeRUTQw",
					"type": "arrow"
				},
				{
					"id": "w7IEkJFMpmZAgwUDktcy8",
					"type": "arrow"
				},
				{
					"type": "text",
					"id": "Ip4sLVub"
				}
			],
			"updated": 1711591207202,
			"link": null,
			"locked": false
		},
		{
			"id": "Ip4sLVub",
			"type": "text",
			"x": 247.85285580287916,
			"y": 33.62114653307347,
			"width": 84.03196716308594,
			"height": 60,
			"angle": 0,
			"strokeColor": "#1e1e1e",
			"backgroundColor": "transparent",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"groupIds": [
				"Z1X4KnfgbIEnb87--WOIB"
			],
			"frameId": null,
			"roundness": null,
			"seed": 796037384,
			"version": 312,
			"versionNonce": 1202648328,
			"isDeleted": false,
			"boundElements": null,
			"updated": 1711591207202,
			"link": null,
			"locked": false,
			"text": "Feed\nGeneration\nService",
			"rawText": "Feed Generation\nService",
			"fontSize": 16,
			"fontFamily": 1,
			"textAlign": "center",
			"verticalAlign": "middle",
			"baseline": 54,
			"containerId": "AEWwLZQGGSSWESQ1z96_d",
			"originalText": "Feed Generation\nService",
			"lineHeight": 1.25
		},
		{
			"id": "Bfq78JIFT_XNscww5ZpxX",
			"type": "arrow",
			"x": 939.0800243136877,
			"y": 399.90988486090066,
			"width": 166.38449603519337,
			"height": 33.51335287504696,
			"angle": 0,
			"strokeColor": "#1e1e1e",
			"backgroundColor": "transparent",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"groupIds": [],
			"frameId": null,
			"roundness": {
				"type": 2
			},
			"seed": 1546274056,
			"version": 1711,
			"versionNonce": 1810095880,
			"isDeleted": false,
			"boundElements": [
				{
					"type": "text",
					"id": "BlEy0jz0"
				}
			],
			"updated": 1711590303629,
			"link": null,
			"locked": false,
			"points": [
				[
					0,
					0
				],
				[
					-166.38449603519337,
					-33.51335287504696
				]
			],
			"lastCommittedPoint": [
				103.18086802233938,
				50.51353167166371
			],
			"startBinding": null,
			"endBinding": null,
			"startArrowhead": "arrow",
			"endArrowhead": "arrow"
		},
		{
			"id": "BlEy0jz0",
			"type": "text",
			"x": 836.5692056183132,
			"y": 349.1599459141031,
			"width": 86.30393981933594,
			"height": 40,
			"angle": 0,
			"strokeColor": "#1e1e1e",
			"backgroundColor": "transparent",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"seed": 1894480136,
			"version": 37,
			"versionNonce": 1209954424,
			"isDeleted": false,
			"boundElements": null,
			"updated": 1711590183606,
			"link": null,
			"locked": false,
			"text": "user ids\nare shared",
			"rawText": "user ids\nare shared",
			"fontSize": 16,
			"fontFamily": 1,
			"textAlign": "center",
			"verticalAlign": "middle",
			"baseline": 34,
			"containerId": "Bfq78JIFT_XNscww5ZpxX",
			"originalText": "user ids\nare shared",
			"lineHeight": 1.25
		},
		{
			"id": "mdmXmJQX9zIgdEWBkjYyq",
			"type": "arrow",
			"x": 222.37716827075303,
			"y": 540.3223235018086,
			"width": 206.29590496986827,
			"height": 0,
			"angle": 0,
			"strokeColor": "#f08c00",
			"backgroundColor": "transparent",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"groupIds": [],
			"frameId": null,
			"roundness": {
				"type": 2
			},
			"seed": 1853184888,
			"version": 232,
			"versionNonce": 1343465480,
			"isDeleted": false,
			"boundElements": [
				{
					"type": "text",
					"id": "CREfdNuX"
				}
			],
			"updated": 1711590632156,
			"link": null,
			"locked": false,
			"points": [
				[
					0,
					0
				],
				[
					206.29590496986827,
					0
				]
			],
			"lastCommittedPoint": [
				206.29590496986827,
				0
			],
			"startBinding": {
				"elementId": "5bYSm2V2fEX5_z-MuwxYP",
				"focus": -0.45527096283018675,
				"gap": 15.381137675977797
			},
			"endBinding": {
				"elementId": "ql6LG2EuU-F-mYLltKJvg",
				"focus": 0.23046282139142527,
				"gap": 12.634459439250122
			},
			"startArrowhead": null,
			"endArrowhead": "arrow"
		},
		{
			"id": "CREfdNuX",
			"type": "text",
			"x": 404.74538990671596,
			"y": 530.3223235018086,
			"width": 102.31993103027344,
			"height": 20,
			"angle": 0,
			"strokeColor": "#f08c00",
			"backgroundColor": "transparent",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"seed": 363294728,
			"version": 15,
			"versionNonce": 1107113848,
			"isDeleted": false,
			"boundElements": null,
			"updated": 1711590215610,
			"link": null,
			"locked": false,
			"text": "request feed",
			"rawText": "request feed",
			"fontSize": 16,
			"fontFamily": 1,
			"textAlign": "center",
			"verticalAlign": "middle",
			"baseline": 14,
			"containerId": "mdmXmJQX9zIgdEWBkjYyq",
			"originalText": "request feed",
			"lineHeight": 1.25
		},
		{
			"id": "cBmfK-bBHpP80_3GqBKEF",
			"type": "arrow",
			"x": 605.2536649810716,
			"y": 509.44359955123207,
			"width": 97.94467825837592,
			"height": 152.1252063074387,
			"angle": 0,
			"strokeColor": "#f08c00",
			"backgroundColor": "transparent",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"groupIds": [],
			"frameId": null,
			"roundness": {
				"type": 2
			},
			"seed": 337468168,
			"version": 68,
			"versionNonce": 219435896,
			"isDeleted": false,
			"boundElements": null,
			"updated": 1711590642501,
			"link": null,
			"locked": false,
			"points": [
				[
					0,
					0
				],
				[
					-97.94467825837592,
					-152.1252063074387
				]
			],
			"lastCommittedPoint": [
				-97.87112161691584,
				-152.1252063074387
			],
			"startBinding": {
				"elementId": "NE7r0GWkhpC_qgDFN63wO",
				"focus": 0.2641087190584984,
				"gap": 12.335551507118396
			},
			"endBinding": {
				"elementId": "hbxul81LJulWkIhXVXLND",
				"focus": 0.11758529376629588,
				"gap": 15.593564970224435
			},
			"startArrowhead": null,
			"endArrowhead": "arrow"
		},
		{
			"type": "rectangle",
			"version": 1782,
			"versionNonce": 1340238712,
			"isDeleted": false,
			"id": "hbxul81LJulWkIhXVXLND",
			"fillStyle": "solid",
			"strokeWidth": 1,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": 419.0391783134744,
			"y": 253.48514864634092,
			"strokeColor": "#000000",
			"backgroundColor": "#eeeeee",
			"width": 120.49648094110887,
			"height": 88.23967962722799,
			"seed": 1553383176,
			"groupIds": [
				"PBh1fc-TsqiB2Di8OHbqr",
				"PW9-pksm7Zgt9ZDo6Pw3m"
			],
			"frameId": null,
			"roundness": {
				"type": 1
			},
			"boundElements": [
				{
					"id": "cBmfK-bBHpP80_3GqBKEF",
					"type": "arrow"
				},
				{
					"id": "w7IEkJFMpmZAgwUDktcy8",
					"type": "arrow"
				}
			],
			"updated": 1711590535203,
			"link": null,
			"locked": false
		},
		{
			"type": "line",
			"version": 1909,
			"versionNonce": 1024569608,
			"isDeleted": false,
			"id": "2ur0_EpSJjEG1JtKuWzXw",
			"fillStyle": "solid",
			"strokeWidth": 1,
			"strokeStyle": "dotted",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": 439.9082126282408,
			"y": 283.80874478052635,
			"strokeColor": "#000000",
			"backgroundColor": "#868e96",
			"width": 0.032933835894282115,
			"height": 16.860641405570814,
			"seed": 838145288,
			"groupIds": [
				"PBh1fc-TsqiB2Di8OHbqr",
				"PW9-pksm7Zgt9ZDo6Pw3m"
			],
			"frameId": null,
			"roundness": {
				"type": 2
			},
			"boundElements": [],
			"updated": 1711590226963,
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
			"version": 1803,
			"versionNonce": 1220956168,
			"isDeleted": false,
			"id": "Kw9hSSn7bxR-8dMn_npec",
			"fillStyle": "solid",
			"strokeWidth": 1,
			"strokeStyle": "dotted",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": 501.4799929214962,
			"y": 285.3604819780868,
			"strokeColor": "#000000",
			"backgroundColor": "#868e96",
			"width": 0.08245824850372045,
			"height": 15.865000927991385,
			"seed": 329069576,
			"groupIds": [
				"PBh1fc-TsqiB2Di8OHbqr",
				"PW9-pksm7Zgt9ZDo6Pw3m"
			],
			"frameId": null,
			"roundness": {
				"type": 2
			},
			"boundElements": [],
			"updated": 1711590226963,
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
			"version": 617,
			"versionNonce": 1385107208,
			"isDeleted": false,
			"id": "Z6GYremN",
			"fillStyle": "solid",
			"strokeWidth": 1,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": 434.3018765502386,
			"y": 261.65876227408114,
			"strokeColor": "#000000",
			"backgroundColor": "transparent",
			"width": 9.995544019949598,
			"height": 8.17817237995874,
			"seed": 1760129800,
			"groupIds": [
				"PBh1fc-TsqiB2Di8OHbqr",
				"PW9-pksm7Zgt9ZDo6Pw3m"
			],
			"frameId": null,
			"roundness": null,
			"boundElements": [
				{
					"type": "arrow",
					"id": "kK9JpbpFr2xtb9Hzzo37g"
				},
				{
					"type": "arrow",
					"id": "RI9tfUkQT8R2TTpYlb1Hg"
				}
			],
			"updated": 1711590226963,
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
			"version": 690,
			"versionNonce": 1002048520,
			"isDeleted": false,
			"id": "eJnyr4vf",
			"fillStyle": "solid",
			"strokeWidth": 1,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": 434.90766709689956,
			"y": 301.7921040263053,
			"strokeColor": "#000000",
			"backgroundColor": "transparent",
			"width": 9.995544019949598,
			"height": 8.17817237995874,
			"seed": 1750454792,
			"groupIds": [
				"PBh1fc-TsqiB2Di8OHbqr",
				"PW9-pksm7Zgt9ZDo6Pw3m"
			],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1711590226963,
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
			"version": 589,
			"versionNonce": 665537288,
			"isDeleted": false,
			"id": "JQ9449Io",
			"fillStyle": "solid",
			"strokeWidth": 1,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": 491.98401064169525,
			"y": 261.95200592238905,
			"strokeColor": "#000000",
			"backgroundColor": "transparent",
			"width": 15.44765893992209,
			"height": 8.17817237995874,
			"seed": 417222920,
			"groupIds": [
				"PBh1fc-TsqiB2Di8OHbqr",
				"PW9-pksm7Zgt9ZDo6Pw3m"
			],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1711590226963,
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
			"version": 696,
			"versionNonce": 555526664,
			"isDeleted": false,
			"id": "VMxkYEPI",
			"fillStyle": "solid",
			"strokeWidth": 1,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": 491.6811153683673,
			"y": 302.4976061319677,
			"strokeColor": "#000000",
			"backgroundColor": "transparent",
			"width": 15.44765893992209,
			"height": 8.17817237995874,
			"seed": 1107226632,
			"groupIds": [
				"PBh1fc-TsqiB2Di8OHbqr",
				"PW9-pksm7Zgt9ZDo6Pw3m"
			],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1711590226963,
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
			"type": "rectangle",
			"version": 1447,
			"versionNonce": 82574600,
			"isDeleted": false,
			"id": "FFiqvPySpqtJd6EImeEg9",
			"fillStyle": "solid",
			"strokeWidth": 1,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": 426.77014722341505,
			"y": 260.4163621518027,
			"strokeColor": "#000000",
			"backgroundColor": "#868e96",
			"width": 25.05900267359336,
			"height": 9.863649988542074,
			"seed": 276405768,
			"groupIds": [
				"hep5sKOQUXN2RqY1PbSIS",
				"PBh1fc-TsqiB2Di8OHbqr",
				"PW9-pksm7Zgt9ZDo6Pw3m"
			],
			"frameId": null,
			"roundness": null,
			"boundElements": [
				{
					"type": "arrow",
					"id": "kK9JpbpFr2xtb9Hzzo37g"
				}
			],
			"updated": 1711590226962,
			"link": null,
			"locked": false
		},
		{
			"type": "rectangle",
			"version": 1788,
			"versionNonce": 930552840,
			"isDeleted": false,
			"id": "GSD2BDQsVYhAHFwn7O7ho",
			"fillStyle": "solid",
			"strokeWidth": 1,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": 466.6512833933007,
			"y": 260.0068328245417,
			"strokeColor": "#000000",
			"backgroundColor": "#ced4da",
			"width": 66.11311343671451,
			"height": 10.663405393018481,
			"seed": 581475592,
			"groupIds": [
				"hep5sKOQUXN2RqY1PbSIS",
				"PBh1fc-TsqiB2Di8OHbqr",
				"PW9-pksm7Zgt9ZDo6Pw3m"
			],
			"frameId": null,
			"roundness": {
				"type": 1
			},
			"boundElements": [
				{
					"type": "arrow",
					"id": "kK9JpbpFr2xtb9Hzzo37g"
				}
			],
			"updated": 1711590226962,
			"link": null,
			"locked": false
		},
		{
			"type": "arrow",
			"version": 7172,
			"versionNonce": 264806520,
			"isDeleted": false,
			"id": "kK9JpbpFr2xtb9Hzzo37g",
			"fillStyle": "solid",
			"strokeWidth": 1,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": 453.39014143980035,
			"y": 265.75747126618876,
			"strokeColor": "#000000",
			"backgroundColor": "#ced4da",
			"width": 14.110644515372014,
			"height": 0.1286692574004148,
			"seed": 882883592,
			"groupIds": [
				"hep5sKOQUXN2RqY1PbSIS",
				"PBh1fc-TsqiB2Di8OHbqr",
				"PW9-pksm7Zgt9ZDo6Pw3m"
			],
			"frameId": null,
			"roundness": {
				"type": 2
			},
			"boundElements": [],
			"updated": 1711590227546,
			"link": null,
			"locked": false,
			"startBinding": {
				"elementId": "Z6GYremN",
				"focus": 0.0334025877122582,
				"gap": 9.092720869612123
			},
			"endBinding": {
				"elementId": "6fTQc9hf7XGbzDa1CL8et",
				"focus": 2.4561325923760253,
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
			"version": 1520,
			"versionNonce": 2094381576,
			"isDeleted": false,
			"id": "K6y1BtLg1x1P_eqLgoeaa",
			"fillStyle": "solid",
			"strokeWidth": 1,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": 427.1966834391367,
			"y": 273.6389848391458,
			"strokeColor": "#000000",
			"backgroundColor": "#868e96",
			"width": 25.05900267359336,
			"height": 9.863649988542074,
			"seed": 1482357512,
			"groupIds": [
				"kp1il1-zVUX2XTlXWA0F7",
				"PBh1fc-TsqiB2Di8OHbqr",
				"PW9-pksm7Zgt9ZDo6Pw3m"
			],
			"frameId": null,
			"roundness": null,
			"boundElements": [
				{
					"type": "arrow",
					"id": "RI9tfUkQT8R2TTpYlb1Hg"
				},
				{
					"type": "arrow",
					"id": "kK9JpbpFr2xtb9Hzzo37g"
				}
			],
			"updated": 1711590226962,
			"link": null,
			"locked": false
		},
		{
			"type": "rectangle",
			"version": 1872,
			"versionNonce": 1436866568,
			"isDeleted": false,
			"id": "6fTQc9hf7XGbzDa1CL8et",
			"fillStyle": "solid",
			"strokeWidth": 1,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": 467.07781960901957,
			"y": 273.83524605854666,
			"strokeColor": "#000000",
			"backgroundColor": "#ced4da",
			"width": 66.11311343671451,
			"height": 10.663405393018481,
			"seed": 5659144,
			"groupIds": [
				"kp1il1-zVUX2XTlXWA0F7",
				"PBh1fc-TsqiB2Di8OHbqr",
				"PW9-pksm7Zgt9ZDo6Pw3m"
			],
			"frameId": null,
			"roundness": {
				"type": 1
			},
			"boundElements": [
				{
					"type": "arrow",
					"id": "RI9tfUkQT8R2TTpYlb1Hg"
				},
				{
					"type": "arrow",
					"id": "kK9JpbpFr2xtb9Hzzo37g"
				}
			],
			"updated": 1711590226962,
			"link": null,
			"locked": false
		},
		{
			"type": "arrow",
			"version": 7923,
			"versionNonce": 1241834104,
			"isDeleted": false,
			"id": "RI9tfUkQT8R2TTpYlb1Hg",
			"fillStyle": "solid",
			"strokeWidth": 1,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": 453.09193979868496,
			"y": 279.2543756507122,
			"strokeColor": "#000000",
			"backgroundColor": "#ced4da",
			"width": 14.105872619241076,
			"height": 0.026745107590664598,
			"seed": 1871567112,
			"groupIds": [
				"kp1il1-zVUX2XTlXWA0F7",
				"PBh1fc-TsqiB2Di8OHbqr",
				"PW9-pksm7Zgt9ZDo6Pw3m"
			],
			"frameId": null,
			"roundness": {
				"type": 2
			},
			"boundElements": [],
			"updated": 1711590227547,
			"link": null,
			"locked": false,
			"startBinding": {
				"elementId": "Z6GYremN",
				"focus": 3.289050236557551,
				"gap": 9.41744099667224
			},
			"endBinding": {
				"elementId": "K6y1BtLg1x1P_eqLgoeaa",
				"focus": -0.1328247803196019,
				"gap": 14.942126305196041
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
			"version": 1658,
			"versionNonce": 316175624,
			"isDeleted": false,
			"id": "7Zzp4vIxC_De5czLZHb-A",
			"fillStyle": "solid",
			"strokeWidth": 1,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": 427.7831707357493,
			"y": 301.29143676936826,
			"strokeColor": "#000000",
			"backgroundColor": "#868e96",
			"width": 25.05900267359336,
			"height": 9.863649988542074,
			"seed": 696088584,
			"groupIds": [
				"T4e47eaeD0kotwFbzulhh",
				"PBh1fc-TsqiB2Di8OHbqr",
				"PW9-pksm7Zgt9ZDo6Pw3m"
			],
			"frameId": null,
			"roundness": null,
			"boundElements": [
				{
					"type": "arrow",
					"id": "TGV8M_VVJHZieeHPhZajk"
				}
			],
			"updated": 1711590226962,
			"link": null,
			"locked": false
		},
		{
			"type": "rectangle",
			"version": 1993,
			"versionNonce": 1091867656,
			"isDeleted": false,
			"id": "p-wrJOG-Tpt-fonFIfh_C",
			"fillStyle": "solid",
			"strokeWidth": 1,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": 467.66430690563743,
			"y": 301.18480271543774,
			"strokeColor": "#000000",
			"backgroundColor": "#ced4da",
			"width": 66.11311343671451,
			"height": 10.663405393018481,
			"seed": 1646343944,
			"groupIds": [
				"T4e47eaeD0kotwFbzulhh",
				"PBh1fc-TsqiB2Di8OHbqr",
				"PW9-pksm7Zgt9ZDo6Pw3m"
			],
			"frameId": null,
			"roundness": {
				"type": 1
			},
			"boundElements": [
				{
					"type": "arrow",
					"id": "TGV8M_VVJHZieeHPhZajk"
				}
			],
			"updated": 1711590226963,
			"link": null,
			"locked": false
		},
		{
			"type": "arrow",
			"version": 8839,
			"versionNonce": 1429328760,
			"isDeleted": false,
			"id": "TGV8M_VVJHZieeHPhZajk",
			"fillStyle": "solid",
			"strokeWidth": 1,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": 453.9228261156361,
			"y": 306.91965508060446,
			"strokeColor": "#000000",
			"backgroundColor": "#ced4da",
			"width": 14.110644515372014,
			"height": 0.06608807192479067,
			"seed": 1844778504,
			"groupIds": [
				"T4e47eaeD0kotwFbzulhh",
				"PBh1fc-TsqiB2Di8OHbqr",
				"PW9-pksm7Zgt9ZDo6Pw3m"
			],
			"frameId": null,
			"roundness": {
				"type": 2
			},
			"boundElements": [],
			"updated": 1711590227547,
			"link": null,
			"locked": false,
			"startBinding": {
				"elementId": "komHsex0",
				"focus": -1.3793878506756334,
				"gap": 5.390822366955263
			},
			"endBinding": {
				"elementId": "p-wrJOG-Tpt-fonFIfh_C",
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
			"type": "text",
			"version": 843,
			"versionNonce": 1124739336,
			"isDeleted": false,
			"id": "komHsex0",
			"fillStyle": "solid",
			"strokeWidth": 1,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": 447.9140053221163,
			"y": 312.3104774475597,
			"strokeColor": "#000000",
			"backgroundColor": "transparent",
			"width": 62.7468269238251,
			"height": 27.976292259030313,
			"seed": 1538502408,
			"groupIds": [
				"PW9-pksm7Zgt9ZDo6Pw3m"
			],
			"frameId": null,
			"roundness": null,
			"boundElements": [
				{
					"type": "arrow",
					"id": "TGV8M_VVJHZieeHPhZajk"
				}
			],
			"updated": 1711590226963,
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
			"baseline": 20
		},
		{
			"id": "sOdNYvJL",
			"type": "text",
			"x": 419.420143659112,
			"y": 225.97524220260235,
			"width": 121.96791076660156,
			"height": 20,
			"angle": 0,
			"strokeColor": "#1e1e1e",
			"backgroundColor": "transparent",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"seed": 789315336,
			"version": 81,
			"versionNonce": 199994376,
			"isDeleted": false,
			"boundElements": null,
			"updated": 1711590241082,
			"link": null,
			"locked": false,
			"text": "computed feeds",
			"rawText": "computed feeds",
			"fontSize": 16,
			"fontFamily": 1,
			"textAlign": "left",
			"verticalAlign": "top",
			"baseline": 14,
			"containerId": null,
			"originalText": "computed feeds",
			"lineHeight": 1.25
		},
		{
			"id": "CeiVOZ_eCH2mjH70pPJ9M",
			"type": "arrow",
			"x": 367.4193430662052,
			"y": 90.3913856892756,
			"width": 303.8666296616201,
			"height": 210.21863730541804,
			"angle": 0,
			"strokeColor": "#1e1e1e",
			"backgroundColor": "transparent",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"groupIds": [],
			"frameId": null,
			"roundness": {
				"type": 2
			},
			"seed": 1982441848,
			"version": 201,
			"versionNonce": 850319624,
			"isDeleted": false,
			"boundElements": [
				{
					"type": "text",
					"id": "lfs0JnJB"
				}
			],
			"updated": 1711591428654,
			"link": null,
			"locked": false,
			"points": [
				[
					0,
					0
				],
				[
					177.72519645364832,
					88.03721366365947
				],
				[
					303.8666296616201,
					210.21863730541804
				]
			],
			"lastCommittedPoint": [
				309.2104901148434,
				224.86724992941657
			],
			"startBinding": {
				"elementId": "SK68WW9xyedBMNGyVuCDe",
				"gap": 19.178830926874866,
				"focus": -0.29719083087895654
			},
			"endBinding": {
				"elementId": "8NAClcOLd6jYbRqphFtsf",
				"focus": -1.0334492117065963,
				"gap": 11.277138680525415
			},
			"startArrowhead": "arrow",
			"endArrowhead": null
		},
		{
			"id": "lfs0JnJB",
			"type": "text",
			"x": 497.30457369954104,
			"y": 158.42859935293507,
			"width": 95.679931640625,
			"height": 40,
			"angle": 0,
			"strokeColor": "#1e1e1e",
			"backgroundColor": "transparent",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"seed": 1994617720,
			"version": 30,
			"versionNonce": 631923208,
			"isDeleted": false,
			"boundElements": null,
			"updated": 1711590499854,
			"link": null,
			"locked": false,
			"text": "listen to \nimage writes",
			"rawText": "listen to \nimage writes",
			"fontSize": 16,
			"fontFamily": 1,
			"textAlign": "center",
			"verticalAlign": "middle",
			"baseline": 34,
			"containerId": "CeiVOZ_eCH2mjH70pPJ9M",
			"originalText": "listen to \nimage writes",
			"lineHeight": 1.25
		},
		{
			"id": "uzvve57SlzjrBxqeRUTQw",
			"type": "arrow",
			"x": 364.7447040029896,
			"y": 62.07099205093971,
			"width": 644.0667508882179,
			"height": 262.6322727744417,
			"angle": 0,
			"strokeColor": "#1e1e1e",
			"backgroundColor": "transparent",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"groupIds": [],
			"frameId": null,
			"roundness": {
				"type": 2
			},
			"seed": 290350200,
			"version": 322,
			"versionNonce": 1618901000,
			"isDeleted": false,
			"boundElements": [
				{
					"type": "text",
					"id": "c3NY1JvM"
				}
			],
			"updated": 1711591428654,
			"link": null,
			"locked": false,
			"points": [
				[
					0,
					0
				],
				[
					586.7268177404114,
					17.35125008075798
				],
				[
					644.0667508882179,
					262.6322727744417
				]
			],
			"lastCommittedPoint": [
				644.0667508882179,
				262.6322727744417
			],
			"startBinding": {
				"elementId": "SK68WW9xyedBMNGyVuCDe",
				"gap": 16.50419186365923,
				"focus": -0.3636624772540935
			},
			"endBinding": {
				"elementId": "4b9u6XmI0CNhnE31Y3n1w",
				"focus": 0.5935462455695203,
				"gap": 12.070446089926467
			},
			"startArrowhead": null,
			"endArrowhead": "arrow"
		},
		{
			"id": "c3NY1JvM",
			"type": "text",
			"x": 863.8075660549245,
			"y": 49.422242131697686,
			"width": 175.32791137695312,
			"height": 60,
			"angle": 0,
			"strokeColor": "#1e1e1e",
			"backgroundColor": "transparent",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"seed": 1645665544,
			"version": 67,
			"versionNonce": 612903544,
			"isDeleted": false,
			"boundElements": null,
			"updated": 1711590526721,
			"link": null,
			"locked": false,
			"text": "find all followers\nwho need to have this\nimage in their feed",
			"rawText": "find all followers\nwho need to have this\nimage in their feed",
			"fontSize": 16,
			"fontFamily": 1,
			"textAlign": "center",
			"verticalAlign": "middle",
			"baseline": 54,
			"containerId": "uzvve57SlzjrBxqeRUTQw",
			"originalText": "find all followers\nwho need to have this\nimage in their feed",
			"lineHeight": 1.25
		},
		{
			"id": "w7IEkJFMpmZAgwUDktcy8",
			"type": "arrow",
			"x": 307.4138418989216,
			"y": 136.25696317681076,
			"width": 96.6158798615233,
			"height": 142.4048038127844,
			"angle": 0,
			"strokeColor": "#1e1e1e",
			"backgroundColor": "transparent",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"groupIds": [],
			"frameId": null,
			"roundness": {
				"type": 2
			},
			"seed": 357775112,
			"version": 150,
			"versionNonce": 285357832,
			"isDeleted": false,
			"boundElements": [
				{
					"type": "text",
					"id": "8QCAbsAq"
				}
			],
			"updated": 1711591428655,
			"link": null,
			"locked": false,
			"points": [
				[
					0,
					0
				],
				[
					8.2719555523027,
					82.34069469623893
				],
				[
					96.6158798615233,
					142.4048038127844
				]
			],
			"lastCommittedPoint": [
				96.61587986152324,
				142.40480381278442
			],
			"startBinding": {
				"elementId": "SK68WW9xyedBMNGyVuCDe",
				"gap": 8.354914989712938,
				"focus": -0.03838871741532094
			},
			"endBinding": {
				"elementId": "hbxul81LJulWkIhXVXLND",
				"focus": -0.37873702318389896,
				"gap": 15.009456553029509
			},
			"startArrowhead": null,
			"endArrowhead": "arrow"
		},
		{
			"id": "8QCAbsAq",
			"type": "text",
			"x": 288.99382315048405,
			"y": 187.45936508320295,
			"width": 133.45591735839844,
			"height": 40,
			"angle": 0,
			"strokeColor": "#1e1e1e",
			"backgroundColor": "transparent",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"seed": 745653768,
			"version": 38,
			"versionNonce": 13657208,
			"isDeleted": false,
			"boundElements": null,
			"updated": 1711590542370,
			"link": null,
			"locked": false,
			"text": "write post_id\nto correct feeds",
			"rawText": "write post_id\nto correct feeds",
			"fontSize": 16,
			"fontFamily": 1,
			"textAlign": "center",
			"verticalAlign": "middle",
			"baseline": 34,
			"containerId": "w7IEkJFMpmZAgwUDktcy8",
			"originalText": "write post_id\nto correct feeds",
			"lineHeight": 1.25
		},
		{
			"type": "rectangle",
			"version": 1880,
			"versionNonce": 348866936,
			"isDeleted": false,
			"id": "ql6LG2EuU-F-mYLltKJvg",
			"fillStyle": "solid",
			"strokeWidth": 1,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 90,
			"angle": 0,
			"x": 441.30753267987143,
			"y": 462.67899217326146,
			"strokeColor": "#000000",
			"backgroundColor": "#eeeeee",
			"width": 69.69390497296568,
			"height": 201.7922810927382,
			"seed": 733427064,
			"groupIds": [
				"1yK4FKmiBQnq7K4FJBMEs",
				"-Az-qsL2Kj08wEybBMe0f"
			],
			"frameId": null,
			"roundness": null,
			"boundElements": [
				{
					"id": "OYX5n8TJFSoUeiR6gmBqV",
					"type": "arrow"
				},
				{
					"id": "zz4n1wx0QcbUHZHH6NdMp",
					"type": "arrow"
				},
				{
					"id": "mdmXmJQX9zIgdEWBkjYyq",
					"type": "arrow"
				},
				{
					"id": "X9vAp0L3eWEitFELhVhsM",
					"type": "arrow"
				}
			],
			"updated": 1711590641080,
			"link": null,
			"locked": false
		},
		{
			"type": "ellipse",
			"version": 1694,
			"versionNonce": 64154232,
			"isDeleted": false,
			"id": "ANRjtCOxqkBgYghA9hO11",
			"fillStyle": "solid",
			"strokeWidth": 1,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": 484.43927827248945,
			"y": 532.5634431857272,
			"strokeColor": "#000000",
			"backgroundColor": "#868e96",
			"width": 18.463181339628875,
			"height": 17.895083452255665,
			"seed": 320980600,
			"groupIds": [
				"L7YB5BZVxHmuwCDUPRTVW",
				"1yK4FKmiBQnq7K4FJBMEs",
				"-Az-qsL2Kj08wEybBMe0f"
			],
			"frameId": null,
			"roundness": {
				"type": 2
			},
			"boundElements": [
				{
					"type": "arrow",
					"id": "wnM0f9ETZnwYn0pr427tv"
				},
				{
					"type": "arrow",
					"id": "5_26wTfciQJq5Pkl_mxa4"
				}
			],
			"updated": 1711590631061,
			"link": null,
			"locked": false
		},
		{
			"type": "ellipse",
			"version": 2003,
			"versionNonce": 1132768376,
			"isDeleted": false,
			"id": "oTF7fog9R7uVwZuIr97IX",
			"fillStyle": "solid",
			"strokeWidth": 1,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": 448.37551935890406,
			"y": 529.6715080105764,
			"strokeColor": "#000000",
			"backgroundColor": "#868e96",
			"width": 18.463181339628875,
			"height": 17.895083452255665,
			"seed": 823277432,
			"groupIds": [
				"L7YB5BZVxHmuwCDUPRTVW",
				"1yK4FKmiBQnq7K4FJBMEs",
				"-Az-qsL2Kj08wEybBMe0f"
			],
			"frameId": null,
			"roundness": {
				"type": 2
			},
			"boundElements": [
				{
					"type": "arrow",
					"id": "B7FSLW6QRk75rnTxdvXVm"
				},
				{
					"type": "arrow",
					"id": "wnM0f9ETZnwYn0pr427tv"
				},
				{
					"type": "arrow",
					"id": "5_26wTfciQJq5Pkl_mxa4"
				}
			],
			"updated": 1711590631061,
			"link": null,
			"locked": false
		},
		{
			"type": "ellipse",
			"version": 2001,
			"versionNonce": 250523768,
			"isDeleted": false,
			"id": "1zH1_GPjRUtjWPnTdrGRa",
			"fillStyle": "solid",
			"strokeWidth": 1,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": 484.93103376926047,
			"y": 583.1630847825041,
			"strokeColor": "#000000",
			"backgroundColor": "#868e96",
			"width": 18.463181339628875,
			"height": 17.895083452255665,
			"seed": 2043447416,
			"groupIds": [
				"L7YB5BZVxHmuwCDUPRTVW",
				"1yK4FKmiBQnq7K4FJBMEs",
				"-Az-qsL2Kj08wEybBMe0f"
			],
			"frameId": null,
			"roundness": {
				"type": 2
			},
			"boundElements": [
				{
					"type": "arrow",
					"id": "5_26wTfciQJq5Pkl_mxa4"
				}
			],
			"updated": 1711590631061,
			"link": null,
			"locked": false
		},
		{
			"type": "ellipse",
			"version": 1718,
			"versionNonce": 934404472,
			"isDeleted": false,
			"id": "LvNYelAHCvuJa8jWJPvEc",
			"fillStyle": "solid",
			"strokeWidth": 1,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": 484.24931630442507,
			"y": 480.9785025785636,
			"strokeColor": "#000000",
			"backgroundColor": "#868e96",
			"width": 18.463181339628875,
			"height": 17.895083452255665,
			"seed": 957659512,
			"groupIds": [
				"L7YB5BZVxHmuwCDUPRTVW",
				"1yK4FKmiBQnq7K4FJBMEs",
				"-Az-qsL2Kj08wEybBMe0f"
			],
			"frameId": null,
			"roundness": {
				"type": 2
			},
			"boundElements": [
				{
					"type": "arrow",
					"id": "wnM0f9ETZnwYn0pr427tv"
				}
			],
			"updated": 1711590631061,
			"link": null,
			"locked": false
		},
		{
			"type": "arrow",
			"version": 5731,
			"versionNonce": 683623944,
			"isDeleted": false,
			"id": "B7FSLW6QRk75rnTxdvXVm",
			"fillStyle": "solid",
			"strokeWidth": 1,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": 461.4446516031169,
			"y": 547.8865959306247,
			"strokeColor": "#000000",
			"backgroundColor": "transparent",
			"width": 26.68308902555831,
			"height": 37.58197677119037,
			"seed": 573491832,
			"groupIds": [
				"L7YB5BZVxHmuwCDUPRTVW",
				"1yK4FKmiBQnq7K4FJBMEs",
				"-Az-qsL2Kj08wEybBMe0f"
			],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1711590632156,
			"link": null,
			"locked": false,
			"startBinding": {
				"elementId": "oTF7fog9R7uVwZuIr97IX",
				"focus": 0.24472012017708783,
				"gap": 1.0429565441459019
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
			"version": 4362,
			"versionNonce": 1704682504,
			"isDeleted": false,
			"id": "5_26wTfciQJq5Pkl_mxa4",
			"fillStyle": "solid",
			"strokeWidth": 1,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": 467.42994348875027,
			"y": 538.8945302216241,
			"strokeColor": "#000000",
			"backgroundColor": "transparent",
			"width": 16.61130383973117,
			"height": 1.3207328297184937,
			"seed": 1608432504,
			"groupIds": [
				"L7YB5BZVxHmuwCDUPRTVW",
				"1yK4FKmiBQnq7K4FJBMEs",
				"-Az-qsL2Kj08wEybBMe0f"
			],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1711590632156,
			"link": null,
			"locked": false,
			"startBinding": {
				"elementId": "oTF7fog9R7uVwZuIr97IX",
				"focus": -0.05630840266133582,
				"gap": 1
			},
			"endBinding": {
				"elementId": "ANRjtCOxqkBgYghA9hO11",
				"focus": 0.059045777174586,
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
			"version": 5319,
			"versionNonce": 344457736,
			"isDeleted": false,
			"id": "wnM0f9ETZnwYn0pr427tv",
			"fillStyle": "solid",
			"strokeWidth": 1,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": 462.9664466636864,
			"y": 530.4404238222385,
			"strokeColor": "#000000",
			"backgroundColor": "transparent",
			"width": 25.400417044718434,
			"height": 32.52973567190321,
			"seed": 610831480,
			"groupIds": [
				"L7YB5BZVxHmuwCDUPRTVW",
				"1yK4FKmiBQnq7K4FJBMEs",
				"-Az-qsL2Kj08wEybBMe0f"
			],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1711590632156,
			"link": null,
			"locked": false,
			"startBinding": {
				"elementId": "oTF7fog9R7uVwZuIr97IX",
				"focus": -0.08869372840676369,
				"gap": 1
			},
			"endBinding": {
				"elementId": "LvNYelAHCvuJa8jWJPvEc",
				"focus": -0.09679793421697816,
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
			"version": 773,
			"versionNonce": 2147350136,
			"isDeleted": false,
			"id": "x0tgiCgj",
			"fillStyle": "solid",
			"strokeWidth": 1,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": 444.65448516635433,
			"y": 619.071395498575,
			"strokeColor": "#000000",
			"backgroundColor": "transparent",
			"width": 63,
			"height": 40,
			"seed": 965754232,
			"groupIds": [
				"-Az-qsL2Kj08wEybBMe0f"
			],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1711590631061,
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
			"baseline": 34
		},
		{
			"id": "X9vAp0L3eWEitFELhVhsM",
			"type": "arrow",
			"x": 523.4092893836995,
			"y": 565.5641480394122,
			"width": 39.59619959124234,
			"height": 0,
			"angle": 0,
			"strokeColor": "#1e1e1e",
			"backgroundColor": "transparent",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"groupIds": [],
			"frameId": null,
			"roundness": {
				"type": 2
			},
			"seed": 1039992072,
			"version": 30,
			"versionNonce": 406836600,
			"isDeleted": false,
			"boundElements": null,
			"updated": 1711590642502,
			"link": null,
			"locked": false,
			"points": [
				[
					0,
					0
				],
				[
					39.59619959124234,
					0
				]
			],
			"lastCommittedPoint": null,
			"startBinding": {
				"elementId": "ql6LG2EuU-F-mYLltKJvg",
				"focus": 0.019713492597544225,
				"gap": 12.407851730862376
			},
			"endBinding": {
				"elementId": "NE7r0GWkhpC_qgDFN63wO",
				"focus": 0.07039935969552534,
				"gap": 11.806694799466072
			},
			"startArrowhead": null,
			"endArrowhead": "arrow"
		},
		{
			"id": "vxLVdkeq",
			"type": "text",
			"x": 861.4364589465313,
			"y": 651.6168296340742,
			"width": 303.85577392578125,
			"height": 100,
			"angle": 0,
			"strokeColor": "#1e1e1e",
			"backgroundColor": "transparent",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"seed": 1843930632,
			"version": 369,
			"versionNonce": 541907832,
			"isDeleted": false,
			"boundElements": [],
			"updated": 1711591156248,
			"link": null,
			"locked": false,
			"text": "replicate object storage for durability\n\nshard photo storage by geography,\nbecause most access patterns are\nlikely geographically bound.",
			"rawText": "replicate object storage for durability\n\nshard photo storage by geography,\nbecause most access patterns are\nlikely geographically bound.",
			"fontSize": 16,
			"fontFamily": 1,
			"textAlign": "left",
			"verticalAlign": "top",
			"baseline": 94,
			"containerId": null,
			"originalText": "replicate object storage for durability\n\nshard photo storage by geography,\nbecause most access patterns are\nlikely geographically bound.",
			"lineHeight": 1.25
		},
		{
			"type": "line",
			"version": 6540,
			"versionNonce": 1725336440,
			"isDeleted": false,
			"id": "ZSQ8L75FSDWTEjHw8Xddr",
			"fillStyle": "solid",
			"strokeWidth": 1,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": 1005.8617491584364,
			"y": 541.5776743204414,
			"strokeColor": "#000000",
			"backgroundColor": "#ced4da",
			"width": 71.66451803756424,
			"height": 92.4944378166419,
			"seed": 479429896,
			"groupIds": [
				"cAWuEwj0EYHT3DPpkzVVH",
				"TScZwrSZdJh01vSmqVwsd",
				"nJeWo08fl5109unsLIrAm",
				"ACAjyYkDoXldUgvJMAOFr"
			],
			"frameId": null,
			"roundness": {
				"type": 2
			},
			"boundElements": [],
			"updated": 1711591147148,
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
					0.23631277756161562,
					69.90679477501719
				],
				[
					0.011058883236775303,
					77.86537979260234
				],
				[
					3.690881175524461,
					81.30418596549401
				],
				[
					16.505678697187165,
					84.21452947378963
				],
				[
					38.166316523905,
					85.12076696651043
				],
				[
					58.86162358869831,
					83.67382606057318
				],
				[
					69.85719260843815,
					80.2134930539004
				],
				[
					71.40796883026277,
					77.29639602912391
				],
				[
					71.62576973675768,
					70.88899726829273
				],
				[
					71.45482135084606,
					5.864789891179346
				],
				[
					71.06944881668004,
					-0.27879963213419856
				],
				[
					66.4678637859641,
					-3.712492230559498
				],
				[
					56.77790772977523,
					-5.70110529183138
				],
				[
					34.69580711193442,
					-7.373670850131469
				],
				[
					16.99156283916344,
					-6.376316241616809
				],
				[
					3.0672949545182333,
					-2.9934111019973204
				],
				[
					-0.038748300806571497,
					-0.04200446053826079
				],
				[
					0,
					0
				]
			]
		},
		{
			"type": "ellipse",
			"version": 7368,
			"versionNonce": 468081784,
			"isDeleted": false,
			"id": "YNQG4v7OaCNJzWnFfUeua",
			"fillStyle": "solid",
			"strokeWidth": 1,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": 1006.0122542043496,
			"y": 534.3695040574136,
			"strokeColor": "#000000",
			"backgroundColor": "#fff",
			"width": 71.20485008239825,
			"height": 14.40064523308222,
			"seed": 15574024,
			"groupIds": [
				"cAWuEwj0EYHT3DPpkzVVH",
				"TScZwrSZdJh01vSmqVwsd",
				"nJeWo08fl5109unsLIrAm",
				"ACAjyYkDoXldUgvJMAOFr"
			],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1711591147148,
			"link": null,
			"locked": false
		},
		{
			"type": "diamond",
			"version": 1633,
			"versionNonce": 550767992,
			"isDeleted": false,
			"id": "3RWtSYy1TqDP401iV-qB6",
			"fillStyle": "solid",
			"strokeWidth": 1,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": 1048.3386636779956,
			"y": 556.0599173401732,
			"strokeColor": "#000000",
			"backgroundColor": "#868e96",
			"width": 22.14493603658657,
			"height": 25.74992562393783,
			"seed": 850125576,
			"groupIds": [
				"TScZwrSZdJh01vSmqVwsd",
				"nJeWo08fl5109unsLIrAm",
				"ACAjyYkDoXldUgvJMAOFr"
			],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1711591147148,
			"link": null,
			"locked": false
		},
		{
			"type": "ellipse",
			"version": 1840,
			"versionNonce": 2128846456,
			"isDeleted": false,
			"id": "7HYvsqfimltfvKwX8OxBJ",
			"fillStyle": "solid",
			"strokeWidth": 1,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": 1035.978699378503,
			"y": 595.1998042885591,
			"strokeColor": "#000000",
			"backgroundColor": "#868e96",
			"width": 23.68993157402284,
			"height": 22.659934549065266,
			"seed": 810172936,
			"groupIds": [
				"TScZwrSZdJh01vSmqVwsd",
				"nJeWo08fl5109unsLIrAm",
				"ACAjyYkDoXldUgvJMAOFr"
			],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1711591147148,
			"link": null,
			"locked": false
		},
		{
			"type": "line",
			"version": 3171,
			"versionNonce": 1993936760,
			"isDeleted": false,
			"id": "Ur83XTlS9ebX1E4SFr9VC",
			"fillStyle": "solid",
			"strokeWidth": 1,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": 1025.1217718923006,
			"y": 569.3614542074024,
			"strokeColor": "#000000",
			"backgroundColor": "#868e96",
			"width": 21.517963614269437,
			"height": 19.662074531243835,
			"seed": 1220854024,
			"groupIds": [
				"TScZwrSZdJh01vSmqVwsd",
				"nJeWo08fl5109unsLIrAm",
				"ACAjyYkDoXldUgvJMAOFr"
			],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1711591147148,
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
					10.48483163908686,
					19.662074531243835
				],
				[
					-11.03313197518258,
					19.42132297980718
				],
				[
					0,
					0
				]
			]
		},
		{
			"type": "rectangle",
			"version": 2311,
			"versionNonce": 999679864,
			"isDeleted": false,
			"id": "fTX7PrlisNciosaOcgqnm",
			"fillStyle": "solid",
			"strokeWidth": 1,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": 283.4876169968951,
			"y": 757.4723487430502,
			"strokeColor": "#000000",
			"backgroundColor": "#ced4da",
			"width": 80.06094019654127,
			"height": 28.566344858859722,
			"seed": 900797560,
			"groupIds": [
				"XMTjSvHnl4RwGh790uuZx",
				"LqOfbm34g8QN5jC9odKgl",
				"OtC0nnUPDbZpov5g9R3S7"
			],
			"frameId": null,
			"roundness": {
				"type": 1
			},
			"boundElements": [],
			"updated": 1711591450132,
			"link": null,
			"locked": false
		},
		{
			"type": "ellipse",
			"version": 2243,
			"versionNonce": 1482307704,
			"isDeleted": false,
			"id": "-kY7VXbNa2ds1gwkW7a0Y",
			"fillStyle": "solid",
			"strokeWidth": 1,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": 305.6641215583768,
			"y": 725.1472742975013,
			"strokeColor": "#000000",
			"backgroundColor": "#ced4da",
			"width": 54.125706048365885,
			"height": 52.24634125501985,
			"seed": 545768824,
			"groupIds": [
				"XMTjSvHnl4RwGh790uuZx",
				"LqOfbm34g8QN5jC9odKgl",
				"OtC0nnUPDbZpov5g9R3S7"
			],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1711591450132,
			"link": null,
			"locked": false
		},
		{
			"type": "ellipse",
			"version": 2653,
			"versionNonce": 1517054328,
			"isDeleted": false,
			"id": "_QhcXTxX_BrQtKTzrsg_S",
			"fillStyle": "solid",
			"strokeWidth": 1,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": 270.3320634434716,
			"y": 748.8272706936614,
			"strokeColor": "#000000",
			"backgroundColor": "#ced4da",
			"width": 37.58729586692073,
			"height": 36.459676990913074,
			"seed": 1063278200,
			"groupIds": [
				"XMTjSvHnl4RwGh790uuZx",
				"LqOfbm34g8QN5jC9odKgl",
				"OtC0nnUPDbZpov5g9R3S7"
			],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1711591450132,
			"link": null,
			"locked": false
		},
		{
			"type": "ellipse",
			"version": 2603,
			"versionNonce": 487619192,
			"isDeleted": false,
			"id": "SfFNyDOnoXHXjx1MozBee",
			"fillStyle": "solid",
			"strokeWidth": 1,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": 290.62920321160436,
			"y": 734.1682253055612,
			"strokeColor": "#000000",
			"backgroundColor": "#ced4da",
			"width": 25.802232947415494,
			"height": 23.194252880341384,
			"seed": 1996408696,
			"groupIds": [
				"XMTjSvHnl4RwGh790uuZx",
				"LqOfbm34g8QN5jC9odKgl",
				"OtC0nnUPDbZpov5g9R3S7"
			],
			"frameId": null,
			"roundness": null,
			"boundElements": [
				{
					"id": "fscKPB-NVypfeIpnDLz5P",
					"type": "arrow"
				}
			],
			"updated": 1711591450132,
			"link": null,
			"locked": false
		},
		{
			"type": "ellipse",
			"version": 2362,
			"versionNonce": 1502604664,
			"isDeleted": false,
			"id": "zWHhSH0IPLe9tIYkUiel9",
			"fillStyle": "solid",
			"strokeWidth": 1,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": 341.74792559062325,
			"y": 755.9688569083754,
			"strokeColor": "#000000",
			"backgroundColor": "#ced4da",
			"width": 31.949201486882664,
			"height": 30.069836693536597,
			"seed": 1940330616,
			"groupIds": [
				"XMTjSvHnl4RwGh790uuZx",
				"LqOfbm34g8QN5jC9odKgl",
				"OtC0nnUPDbZpov5g9R3S7"
			],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1711591450132,
			"link": null,
			"locked": false
		},
		{
			"type": "ellipse",
			"version": 1628,
			"versionNonce": 1965260408,
			"isDeleted": false,
			"id": "1cuP1dx7ImlGdca064Md4",
			"fillStyle": "solid",
			"strokeWidth": 1,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": 275.1114369895912,
			"y": 753.4470771677286,
			"strokeColor": "#ced4da",
			"backgroundColor": "#ced4da",
			"width": 33.104272310112094,
			"height": 32.21755073037689,
			"seed": 958220664,
			"groupIds": [
				"LqOfbm34g8QN5jC9odKgl",
				"OtC0nnUPDbZpov5g9R3S7"
			],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1711591450132,
			"link": null,
			"locked": false
		},
		{
			"type": "ellipse",
			"version": 1336,
			"versionNonce": 1511845752,
			"isDeleted": false,
			"id": "nhKgMf-pSYps49oV0aYUh",
			"fillStyle": "solid",
			"strokeWidth": 1,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": 319.7430898362577,
			"y": 741.0329750514353,
			"strokeColor": "#ced4da",
			"backgroundColor": "#ced4da",
			"width": 39.9024710880816,
			"height": 42.8582096871986,
			"seed": 849697400,
			"groupIds": [
				"LqOfbm34g8QN5jC9odKgl",
				"OtC0nnUPDbZpov5g9R3S7"
			],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1711591450132,
			"link": null,
			"locked": false
		},
		{
			"type": "ellipse",
			"version": 1525,
			"versionNonce": 549470328,
			"isDeleted": false,
			"id": "88eWVr0MnfpeKDs0xqhwa",
			"fillStyle": "solid",
			"strokeWidth": 1,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": 333.6350612521054,
			"y": 756.1072419069312,
			"strokeColor": "#ced4da",
			"backgroundColor": "#ced4da",
			"width": 38.12902792861126,
			"height": 29.261812131259756,
			"seed": 1124289400,
			"groupIds": [
				"LqOfbm34g8QN5jC9odKgl",
				"OtC0nnUPDbZpov5g9R3S7"
			],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1711591450132,
			"link": null,
			"locked": false
		},
		{
			"type": "ellipse",
			"version": 1432,
			"versionNonce": 953250168,
			"isDeleted": false,
			"id": "agJpMIdMbeCSt5-D08xbx",
			"fillStyle": "solid",
			"strokeWidth": 1,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": 300.23521508208614,
			"y": 735.4170717131116,
			"strokeColor": "#ced4da",
			"backgroundColor": "#ced4da",
			"width": 31.921976870465226,
			"height": 32.21755073037693,
			"seed": 1417354360,
			"groupIds": [
				"LqOfbm34g8QN5jC9odKgl",
				"OtC0nnUPDbZpov5g9R3S7"
			],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1711591450132,
			"link": null,
			"locked": false
		},
		{
			"type": "ellipse",
			"version": 1361,
			"versionNonce": 2039775864,
			"isDeleted": false,
			"id": "oBVXtPCUFjY4kIZ46tCdK",
			"fillStyle": "solid",
			"strokeWidth": 1,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": 286.63881752615,
			"y": 743.6931397906396,
			"strokeColor": "#ced4da",
			"backgroundColor": "#ced4da",
			"width": 44.040505126845495,
			"height": 40.19804494799322,
			"seed": 1758514552,
			"groupIds": [
				"LqOfbm34g8QN5jC9odKgl",
				"OtC0nnUPDbZpov5g9R3S7"
			],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1711591450132,
			"link": null,
			"locked": false
		},
		{
			"type": "text",
			"version": 1784,
			"versionNonce": 835548024,
			"isDeleted": false,
			"id": "e7WSgP64",
			"fillStyle": "solid",
			"strokeWidth": 1,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 90,
			"angle": 0,
			"x": 301.81947393018436,
			"y": 747.3910778791769,
			"strokeColor": "#000000",
			"backgroundColor": "#ced4da",
			"width": 51.996738788026796,
			"height": 36.17164437427951,
			"seed": 692608632,
			"groupIds": [
				"OtC0nnUPDbZpov5g9R3S7"
			],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1711591450132,
			"link": null,
			"locked": false,
			"fontSize": 29.50888804373403,
			"fontFamily": 3,
			"text": "CDN",
			"rawText": "",
			"textAlign": "center",
			"verticalAlign": "top",
			"containerId": null,
			"originalText": "CDN",
			"lineHeight": 1.2257881191819515,
			"baseline": 28
		},
		{
			"type": "line",
			"version": 2430,
			"versionNonce": 935347320,
			"isDeleted": false,
			"id": "4JaNvF0wbqg8FRy2Qdq_Y",
			"fillStyle": "solid",
			"strokeWidth": 1,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 6.2747829793837475,
			"x": 365.5322605884585,
			"y": 769.6839673320238,
			"strokeColor": "#000000",
			"backgroundColor": "#868e96",
			"width": 19.607935239410914,
			"height": 6.684861083047653,
			"seed": 1990578040,
			"groupIds": [
				"OtC0nnUPDbZpov5g9R3S7"
			],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1711591450132,
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
					15.270551565484011,
					0.015223322488854274
				],
				[
					15.284965840475566,
					-1.7779125363044153
				],
				[
					19.607935239410914,
					1.6771832861962603
				],
				[
					15.07836123226295,
					4.906948546743237
				],
				[
					15.301439297608816,
					3.285557495183402
				],
				[
					0.10913665350767299,
					3.288130451097015
				],
				[
					0,
					0
				]
			]
		},
		{
			"type": "line",
			"version": 2299,
			"versionNonce": 2033251704,
			"isDeleted": false,
			"id": "l_NIHztGj4BbiWBq1htlW",
			"fillStyle": "solid",
			"strokeWidth": 1,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 6.2747829793837475,
			"x": 366.00770912851885,
			"y": 777.9643163095865,
			"strokeColor": "#000000",
			"backgroundColor": "#868e96",
			"width": 27.18566771282433,
			"height": 7.094666851553434,
			"seed": 2033000568,
			"groupIds": [
				"OtC0nnUPDbZpov5g9R3S7"
			],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1711591450132,
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
					20.92520798613003,
					0.016156566320591037
				],
				[
					20.94495983994325,
					-1.8869049004275888
				],
				[
					27.18566771282433,
					1.7828227136221688
				],
				[
					20.66184993528765,
					5.207761951125845
				],
				[
					20.96753338715831,
					3.4869738593466124
				],
				[
					0.14954975029979456,
					3.489704546612068
				],
				[
					0,
					0
				]
			]
		},
		{
			"type": "line",
			"version": 2498,
			"versionNonce": 191071864,
			"isDeleted": false,
			"id": "rXgL--KhRMNi7ZuZW9lVL",
			"fillStyle": "solid",
			"strokeWidth": 1,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 6.2747829793837475,
			"x": 365.0681055937489,
			"y": 761.8771815179994,
			"strokeColor": "#000000",
			"backgroundColor": "#868e96",
			"width": 15.791652087789885,
			"height": 6.947518862846142,
			"seed": 815944056,
			"groupIds": [
				"OtC0nnUPDbZpov5g9R3S7"
			],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1711591450132,
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
					11.613472151298723,
					0.015821468663688054
				],
				[
					11.624434412909128,
					-1.8477692698490982
				],
				[
					15.791652087789885,
					1.7569001831515187
				],
				[
					11.46730866316013,
					5.0997495929970444
				],
				[
					11.636962711892435,
					3.414651761521064
				],
				[
					0.08299998076442283,
					3.4173258125628116
				],
				[
					0,
					0
				]
			]
		},
		{
			"id": "UpgRunEeqUV8mL9n3tUym",
			"type": "arrow",
			"x": 873.7037304874149,
			"y": 620.9676230895943,
			"width": 477.3736850241447,
			"height": 137.2933426485041,
			"angle": 0,
			"strokeColor": "#1e1e1e",
			"backgroundColor": "#4dabf7",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"seed": 1297467912,
			"version": 173,
			"versionNonce": 12017528,
			"isDeleted": false,
			"boundElements": [],
			"updated": 1711591458923,
			"link": null,
			"locked": false,
			"points": [
				[
					0,
					0
				],
				[
					-477.3736850241447,
					137.2933426485041
				]
			],
			"lastCommittedPoint": [
				-499.03890431825096,
				186.20607942439733
			],
			"startBinding": null,
			"endBinding": null,
			"startArrowhead": null,
			"endArrowhead": "arrow"
		},
		{
			"id": "fscKPB-NVypfeIpnDLz5P",
			"type": "arrow",
			"x": 289.8034854635933,
			"y": 724.289521274474,
			"width": 71.2756103027441,
			"height": 63.198725132084974,
			"angle": 0,
			"strokeColor": "#1e1e1e",
			"backgroundColor": "#4dabf7",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"seed": 555622408,
			"version": 265,
			"versionNonce": 916339832,
			"isDeleted": false,
			"boundElements": null,
			"updated": 1711591450132,
			"link": null,
			"locked": false,
			"points": [
				[
					0,
					0
				],
				[
					-71.2756103027441,
					-63.198725132084974
				]
			],
			"lastCommittedPoint": [
				-83.37134680924447,
				-123.12841000730452
			],
			"startBinding": {
				"elementId": "SfFNyDOnoXHXjx1MozBee",
				"focus": 0.5736491597386487,
				"gap": 13.532647159049137
			},
			"endBinding": {
				"elementId": "46SBldcx",
				"focus": -0.5882576908274153,
				"gap": 10.935934153475387
			},
			"startArrowhead": null,
			"endArrowhead": "arrow"
		},
		{
			"id": "OtRBWdT9",
			"type": "text",
			"x": 256.2884609709995,
			"y": 798.6714952745469,
			"width": 181.63186645507812,
			"height": 120,
			"angle": 0,
			"strokeColor": "#1e1e1e",
			"backgroundColor": "#4dabf7",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"seed": 1871700344,
			"version": 164,
			"versionNonce": 432838264,
			"isDeleted": false,
			"boundElements": null,
			"updated": 1711591492049,
			"link": null,
			"locked": false,
			"text": "User checks CDN\nfirst for photo.\nOn a cache miss,\ngrab from object store\nand write back-through\ninto the CDN cache.",
			"rawText": "User checks CDN\nfirst for photo.\nOn a cache miss,\ngrab from object store\nand write back-through\ninto the CDN cache.",
			"fontSize": 16,
			"fontFamily": 1,
			"textAlign": "left",
			"verticalAlign": "top",
			"baseline": 114,
			"containerId": null,
			"originalText": "User checks CDN\nfirst for photo.\nOn a cache miss,\ngrab from object store\nand write back-through\ninto the CDN cache.",
			"lineHeight": 1.25
		},
		{
			"id": "8CMrt2ku",
			"type": "text",
			"x": 116.45901879746265,
			"y": 433.5012478595493,
			"width": 100.31996154785156,
			"height": 60,
			"angle": 0,
			"strokeColor": "#1e1e1e",
			"backgroundColor": "#4dabf7",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"seed": 1342396536,
			"version": 138,
			"versionNonce": 1070636296,
			"isDeleted": false,
			"boundElements": null,
			"updated": 1711591522759,
			"link": null,
			"locked": false,
			"text": "cache recent\nposts locally\non device.",
			"rawText": "cache recent\nposts locally\non device.",
			"fontSize": 16,
			"fontFamily": 1,
			"textAlign": "left",
			"verticalAlign": "top",
			"baseline": 54,
			"containerId": null,
			"originalText": "cache recent\nposts locally\non device.",
			"lineHeight": 1.25
		},
		{
			"id": "CU4xQvxVwS4CiZ3SzhqQ6",
			"type": "rectangle",
			"x": 874.0155519336151,
			"y": 664.6832499709477,
			"width": 298.1556219772531,
			"height": 125.67596564983296,
			"angle": 0,
			"strokeColor": "#1e1e1e",
			"backgroundColor": "#4dabf7",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"seed": 1948476536,
			"version": 553,
			"versionNonce": 25215864,
			"isDeleted": true,
			"boundElements": null,
			"updated": 1711591086092,
			"link": null,
			"locked": false
		},
		{
			"id": "4alOBStc",
			"type": "text",
			"x": 294.87563943862926,
			"y": 555.1016677794811,
			"width": 10,
			"height": 25,
			"angle": 0,
			"strokeColor": "#1e1e1e",
			"backgroundColor": "transparent",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"groupIds": [
				"hHpxRbaWOi8m-ftuiEbtv",
				"I_wrY3yW5VkiRANBg1lTR"
			],
			"frameId": null,
			"roundness": null,
			"seed": 1187712120,
			"version": 2,
			"versionNonce": 1484526600,
			"isDeleted": true,
			"boundElements": null,
			"updated": 1711589135832,
			"link": null,
			"locked": false,
			"text": "",
			"rawText": "",
			"fontSize": 20,
			"fontFamily": 1,
			"textAlign": "center",
			"verticalAlign": "middle",
			"baseline": 17,
			"containerId": "Fp4GUsYjbYsT-oeTxBm9a",
			"originalText": "",
			"lineHeight": 1.25
		},
		{
			"type": "text",
			"version": 1015,
			"versionNonce": 1748176248,
			"isDeleted": true,
			"id": "NKFOCmWn",
			"fillStyle": "solid",
			"strokeWidth": 1,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": 915.2640549866495,
			"y": 630.5732159078335,
			"strokeColor": "#000000",
			"backgroundColor": "transparent",
			"width": 8.759994506835938,
			"height": 23.654560218277254,
			"seed": 1403139448,
			"groupIds": [
				"11KAHy1xbRp8g0PEz8N5v",
				"3D7FOAwyMVuxnZrYz7c2H"
			],
			"frameId": null,
			"roundness": null,
			"boundElements": null,
			"updated": 1711591139926,
			"link": null,
			"locked": false,
			"fontSize": 17.52189645798314,
			"fontFamily": 1,
			"text": "",
			"rawText": "",
			"textAlign": "center",
			"verticalAlign": "top",
			"containerId": null,
			"originalText": "",
			"lineHeight": 1.350000000000001,
			"baseline": 16
		},
		{
			"type": "text",
			"version": 1024,
			"versionNonce": 1763943944,
			"isDeleted": true,
			"id": "vn3L4BOT",
			"fillStyle": "solid",
			"strokeWidth": 1,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": 995.7124686343038,
			"y": 663.5263019161368,
			"strokeColor": "#000000",
			"backgroundColor": "transparent",
			"width": 132.24085998535156,
			"height": 23.654560218277254,
			"seed": 782949128,
			"groupIds": [
				"TkNjc9CCMXZpLQHh-gdnx"
			],
			"frameId": null,
			"roundness": null,
			"boundElements": null,
			"updated": 1711590743619,
			"link": null,
			"locked": false,
			"fontSize": 17.52189645798314,
			"fontFamily": 1,
			"text": "Object Storage",
			"rawText": "Object Storage",
			"textAlign": "center",
			"verticalAlign": "top",
			"containerId": null,
			"originalText": "Object Storage",
			"lineHeight": 1.350000000000001,
			"baseline": 16
		},
		{
			"id": "sJpv8miB",
			"type": "embeddable",
			"x": 806.5354061126709,
			"y": 442.0081901550293,
			"width": 500,
			"height": 500,
			"angle": 0,
			"strokeColor": "transparent",
			"backgroundColor": "transparent",
			"fillStyle": "hachure",
			"strokeWidth": 1,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"roundness": null,
			"seed": 98875,
			"version": 2,
			"versionNonce": 1204230008,
			"updated": 1711589105932,
			"isDeleted": true,
			"groupIds": [],
			"boundElements": [],
			"link": "file:///Users/rockzhou/Downloads/Architecture%20Components.excalidrawlib",
			"locked": false,
			"scale": [
				1,
				1
			],
			"customData": {
				"mdProps": {
					"useObsidianDefaults": false,
					"backgroundMatchCanvas": false,
					"backgroundMatchElement": true,
					"backgroundColor": "#fff",
					"backgroundOpacity": 60,
					"borderMatchElement": true,
					"borderColor": "#fff",
					"borderOpacity": 0,
					"filenameVisible": false
				}
			}
		},
		{
			"id": "MfZaVtQ2",
			"type": "text",
			"x": 645.6908764308586,
			"y": 257.5272586291962,
			"width": 8,
			"height": 20,
			"angle": 0,
			"strokeColor": "#1e1e1e",
			"backgroundColor": "transparent",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"seed": 80562296,
			"version": 12,
			"versionNonce": 1949011976,
			"isDeleted": true,
			"boundElements": null,
			"updated": 1711589377476,
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
			"id": "zsETniXK",
			"type": "text",
			"x": 541.1445395198535,
			"y": 168.42859935293507,
			"width": 8,
			"height": 20,
			"angle": 0,
			"strokeColor": "#1e1e1e",
			"backgroundColor": "transparent",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"seed": 310110328,
			"version": 2,
			"versionNonce": 462518280,
			"isDeleted": true,
			"boundElements": null,
			"updated": 1711590473308,
			"link": null,
			"locked": false,
			"text": "",
			"rawText": "",
			"fontSize": 16,
			"fontFamily": 1,
			"textAlign": "center",
			"verticalAlign": "middle",
			"baseline": 14,
			"containerId": "CeiVOZ_eCH2mjH70pPJ9M",
			"originalText": "",
			"lineHeight": 1.25
		},
		{
			"id": "QWYKzLal",
			"type": "text",
			"x": 1069.5632584903385,
			"y": 568.9672691152155,
			"width": 8,
			"height": 20,
			"angle": 0,
			"strokeColor": "#1e1e1e",
			"backgroundColor": "transparent",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"seed": 340755720,
			"version": 2,
			"versionNonce": 448299128,
			"isDeleted": true,
			"boundElements": null,
			"updated": 1711590931506,
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
			"type": "text",
			"version": 1045,
			"versionNonce": 1395090552,
			"isDeleted": true,
			"id": "E0gaVMNC",
			"fillStyle": "solid",
			"strokeWidth": 1,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": 1066.5271833457518,
			"y": 630.5732159078335,
			"strokeColor": "#000000",
			"backgroundColor": "transparent",
			"width": 8.759994506835938,
			"height": 23.654560218277254,
			"seed": 194469896,
			"groupIds": [
				"nJeWo08fl5109unsLIrAm",
				"ACAjyYkDoXldUgvJMAOFr"
			],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1711591145408,
			"link": null,
			"locked": false,
			"fontSize": 17.52189645798314,
			"fontFamily": 1,
			"text": "",
			"rawText": "",
			"textAlign": "center",
			"verticalAlign": "top",
			"containerId": null,
			"originalText": "",
			"lineHeight": 1.350000000000001,
			"baseline": 16
		},
		{
			"id": "vN2EKwYf_Ws5S5AexKtIL",
			"type": "arrow",
			"x": 873.2533912586359,
			"y": 666.1987576117413,
			"width": 237.07668180073824,
			"height": 97.2247334639543,
			"angle": 0,
			"strokeColor": "#1e1e1e",
			"backgroundColor": "transparent",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"groupIds": [],
			"frameId": null,
			"roundness": {
				"type": 2
			},
			"seed": 1626031224,
			"version": 30,
			"versionNonce": 1312793208,
			"isDeleted": true,
			"boundElements": null,
			"updated": 1711591004757,
			"link": null,
			"locked": false,
			"points": [
				[
					0,
					0
				],
				[
					237.07668180073824,
					97.2247334639543
				]
			],
			"lastCommittedPoint": null,
			"startBinding": {
				"elementId": "vxLVdkeq",
				"focus": 0.02931223613296229,
				"gap": 14.347560514262966
			},
			"endBinding": null,
			"startArrowhead": null,
			"endArrowhead": "arrow"
		},
		{
			"id": "-DnOa0DX9BrdwTLVieQR1",
			"type": "arrow",
			"x": 393.4799800919467,
			"y": 822.2225703559523,
			"width": 477.85578981615686,
			"height": 204.8283226565104,
			"angle": 0,
			"strokeColor": "#1e1e1e",
			"backgroundColor": "#4dabf7",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"seed": 414586376,
			"version": 135,
			"versionNonce": 1572547592,
			"isDeleted": true,
			"boundElements": [],
			"updated": 1711591439209,
			"link": null,
			"locked": false,
			"points": [
				[
					0,
					0
				],
				[
					477.85578981615686,
					-204.8283226565104
				]
			],
			"lastCommittedPoint": [
				477.85578981615686,
				-204.8283226565104
			],
			"startBinding": null,
			"endBinding": null,
			"startArrowhead": null,
			"endArrowhead": "arrow"
		},
		{
			"id": "jEIaiShK",
			"type": "text",
			"x": 628.4078750000251,
			"y": 709.808409027697,
			"width": 8,
			"height": 20,
			"angle": 0,
			"strokeColor": "#1e1e1e",
			"backgroundColor": "#4dabf7",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"seed": 608620808,
			"version": 2,
			"versionNonce": 2100606584,
			"isDeleted": true,
			"boundElements": null,
			"updated": 1711591437061,
			"link": null,
			"locked": false,
			"text": "",
			"rawText": "",
			"fontSize": 16,
			"fontFamily": 1,
			"textAlign": "center",
			"verticalAlign": "middle",
			"baseline": 14,
			"containerId": "-DnOa0DX9BrdwTLVieQR1",
			"originalText": "",
			"lineHeight": 1.25
		},
		{
			"id": "KRVUib9t",
			"type": "text",
			"x": 631.0168879753426,
			"y": 679.6142944138464,
			"width": 8,
			"height": 20,
			"angle": 0,
			"strokeColor": "#1e1e1e",
			"backgroundColor": "#4dabf7",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"seed": 201750280,
			"version": 2,
			"versionNonce": 1787605112,
			"isDeleted": true,
			"boundElements": null,
			"updated": 1711591458925,
			"link": null,
			"locked": false,
			"text": "",
			"rawText": "",
			"fontSize": 16,
			"fontFamily": 1,
			"textAlign": "center",
			"verticalAlign": "middle",
			"baseline": 14,
			"containerId": "UpgRunEeqUV8mL9n3tUym",
			"originalText": "",
			"lineHeight": 1.25
		}
	],
	"appState": {
		"theme": "dark",
		"viewBackgroundColor": "#ffffff",
		"currentItemStrokeColor": "#1e1e1e",
		"currentItemBackgroundColor": "#eeeeee",
		"currentItemFillStyle": "solid",
		"currentItemStrokeWidth": 2,
		"currentItemStrokeStyle": "solid",
		"currentItemRoughness": 1,
		"currentItemOpacity": 100,
		"currentItemFontFamily": 1,
		"currentItemFontSize": 16,
		"currentItemTextAlign": "left",
		"currentItemStartArrowhead": null,
		"currentItemEndArrowhead": "arrow",
		"scrollX": 869.6082516060717,
		"scrollY": 574.811082463482,
		"zoom": {
			"value": 0.47806538508915924
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