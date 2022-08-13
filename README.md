1    # Credits: @mrismanaziz
2    # Copyright (C) 2022 Pyro-ManUserbot
3    #
4    # This file is a part of < https://github.com/mrismanaziz/PyroMan-Userbot/ >
5    # PLease read the GNU Affero General Public License in
6    # <https://www.github.com/mrismanaziz/PyroMan-Userbot/blob/main/LICENSE/>.
7    #
8    # t.me/SharingUserbot & t.me/Lunatic0de
9    # Meliodas-PyroBot
10
11     import asyncio
12     import logging
13     import sys
14     import time
15     from datetime import datetime
16     from logging.handlers import RotatingFileHandler
17     from typing import Any, Dict
18
19     from aiohttp import ClientSession
20     from apscheduler.schedulers.asyncio import AsyncIOScheduler
21     from gpytranslate import Translator
22     from pyrogram import Client
23     from pyrogram.types import *
24     from pytgcalls import GroupCallFactory
25
26     from config import (
27     API_HASH,
28     API_ID,
29     BOTLOG_CHATID,
30     DB_URL,
31     STRING_SESSION1,
32     STRING_SESSION2,
33     STRING_SESSION3,
34     STRING_SESSION4,
35     STRING_SESSION5,
36     SUDO_USERS,
37  )
38
39     LOOP = asyncio.get_event_loop_policy().get_event_loop()
40     trl = Translator()
41     aiosession = ClientSession()
42     CMD_HELP = {}
43     scheduler = AsyncIOScheduler()
44     StartTime = time.time()
45     START_TIME = datetime.now()
46     TEMP_SETTINGS: Dict[Any, Any] = {}
47     TEMP_SETTINGS["PM_COUNT"] = {}
48     TEMP_SETTINGS["PM_LAST_MSG"] = {}
49
50     LOG_FILE_NAME = "logs.txt"
51     logging.basicConfig(
52     level=logging.INFO,
54     format="[%(levelname)s] - %(name)s - %(message)s",
55     datefmt="%d-%b-%y %H:%M:%S",
56     handlers=[
57     RotatingFileHandler(LOG_FILE_NAME, maxBytes=50000000, backupCount=10),
58     logging.StreamHandler(),
59    ],
60  )
61     logging.getLogger("asyncio").setLevel(logging.CRITICAL)
62     logging.getLogger("pytgcalls").setLevel(logging.WARNING)
63     logging.getLogger("pyrogram").setLevel(logging.WARNING)
64     logging.getLogger("pyrogram.client").setLevel(logging.WARNING)
65     logging.getLogger("pyrogram.syncer").setLevel(logging.CRITICAL)
66     logging.getLogger("pyrogram.session.auth").setLevel(logging.CRITICAL)
67     logging.getLogger("pyrogram.session.session").setLevel(logging.CRITICAL)
68     LOGS = logging.getLogger(name)
69
70
71     def LOGGER(name: str) -> logging.Logger:
72     return logging.getLogger(name)
73
74
75     API_ID = API_ID
76     API_HASH = API_HASH
77     SUDO_USERS = SUDO_USERS
78     DB_URL = DB_URL
79
80     if not STRING_SESSION1:
81     LOGGER(name).error("No String Session Found! Exiting!")
82     sys.exit()
83
84     if not API_ID:
85     LOGGER(name).error("No API_ID Found! Exiting!")
86     sys.exit()
87 
88     if not API_HASH:
89     LOGGER(name).error("No API_HASH Found! Exiting!")
90     sys.exit()
91
92     if BOTLOG_CHATID:
93     BOTLOG_CHATID = BOTLOG_CHATID
94     else:
95     BOTLOG_CHATID = "me"
96
97
98     bot1 = (
99     Client(
100     session_name=STRING_SESSION1,
101     api_id=API_ID,
102     api_hash=API_HASH,
103     plugins=dict(root="Cilik/modules"),
104   )
105    if STRING_SESSION1
106    else None
107 )
108
109   bot2 = (
110   Client(
111     session_name=STRING_SESSION2,
112     api_id=API_ID,
113     api_hash=API_HASH,
114     plugins=dict(root="Cilik/modules"),
115    )
116    if STRING_SESSION2
117    else None
118  )
119
120   bot3 = (
121   Client(
122     session_name=STRING_SESSION3,
123     api_id=API_ID,
124     api_hash=API_HASH,
125     plugins=dict(root="Cilik/modules"),
126    )
127    if STRING_SESSION3
128    else None
129 )
130
131  bot4 = (
132  Client(
133     session_name=STRING_SESSION4,
134     api_id=API_ID,
135     api_hash=API_HASH,
136     plugins=dict(root="Cilik/modules"),
137   )
138    if STRING_SESSION4
139    else None
140 )
141
142  bot5 = (
143  Client(
144     session_name=STRING_SESSION5,
145     api_id=API_ID,
146     api_hash=API_HASH,
147     plugins=dict(root="Cilik/modules"),
148    )
149   if STRING_SESSION5
150   else None
151 )
152
153
154    bots = [bot for bot in [bot1, bot2, bot3, bot4, bot5] if bot]
155
156  for bot in bots:
157  if not hasattr(bot, "group_call"):
158  setattr(bot, "group_call", GroupCallFactory(bot).get_group_call())
