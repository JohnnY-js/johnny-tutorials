 # Sistema de Moderação.
 
 Basicamente, o sistema de moderação será envolvido os comandos.. ban, kick e talvez mute.

# Vamos começar com o comando ban.

 Vamos precisar dos seguintes imports..


import discord #Importa o discord
import asyncio #Importa o asyncio
from discord.ext import commands #Importa os comandos na pasta cogs.

# Vamos criar a class ban.


class ban():
    def __init__(self, client):
        self.client = client
    @commands.command()
    async def ban(self,ctx,member: discord.Member=None):

**Isso é preciso**
