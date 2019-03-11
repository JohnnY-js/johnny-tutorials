 # Sistema de Moderação.
 
 **Basicamente, o sistema de moderação será envolvido os comandos.. ban, kick e talvez mute.**

# Vamos começar com o comando ban com emoji.

 **Vamos precisar dos seguintes imports..**

```Python
import discord #Importa o discord
import asyncio #Importa o asyncio
from discord.ext import commands #Importa os comandos na pasta cogs.
```
# Vamos criar a class ban.

```Python
class ban():
    def __init__(self, client):
        self.client = client
    @commands.command()
    async def ban(self,ctx,member: discord.Member=None):
```
**Isso é preciso o self, ctx e o member.**

JohnnY, como posso setar só para quem tem tal permissão para usar esse comando?
**Simples, só colocar depois do def ban.**
Exemplo:
```Python
if ctx.author.guild_permissions.administrator:
```

# Vamos definir para quando você apenas utilizar o comando e não marcar um membro.

```Python
if member is None:
                await ctx.send(f"Olá {ctx.author.mention} você não marcou um user para banir")
```

# Agora, quando o user não tem permissão..

```Python
else:
            await ctx.send("Você não tem permissão!")
```

