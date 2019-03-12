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
# Agora vamos setar o embed.
```Python
embed = discord.Embed(colour=CorDoEmbed) #Exemplo: 0xff5d00
```
# Ok, agora vamos dar para o administrador 60 segundos para banir.
```
embed.set_author(name=f"Você deseja banir o {member.name}? (60 segundos)")
```
# Agora vamos continuar com o resto dos comandos.
```Python
embed.add_field(name="ID:",value=member.id,inline=False) # Vai pegar o id do player que vai ser punido

embed.add_field(name="Menção:",value=member.mention,inline=False) # Vai mencionar o player punido

embed.add_field(name="Tag:",value=member.discriminator,inline=False) # Vai mostrar a tag do player punido

embed.add_field(name="Criação da Conta:",value=member.created_at.strftime("**%H:%M:%S - %d/%m/20%y**"),inline=False) #Dia de criação de conta do player punido    

embed.add_field(name="Avatar Link:",value="[Link Direto](" + member.avatar_url + ")\n",inline=False) #Vai pegar o link do avatar do player punido   

embed.set_thumbnail(url=member.avatar_url)
```
# Agora vamos fazer para que a mensagem seja postada.
```Python
msg = await ctx.send(embed=embed)
```
# Agora vamos fazer que o bot adicione os emojis
```Python
await msg.add_reaction("✅")
await msg.add_reaction("❌")
```
# Agora vamos fazer o delay e a mensagem para quando o player for banido

```Python
return user == ctx.author and str(reaction.emoji)
        try:
            reaction, user = await self.client.wait_for('reaction_add', timeout=60.0, check=check)
            if reaction.emoji == "✅":
                await member.ban()
                await msg.delete()
                await ctx.send(f"Olá {ctx.author.mention} o {member.name} foi banido com sucesso")
            if reaction.emoji == "❌":
                await msg.delete()
        except asyncio.TimeoutError:
            await msg.delete()
            msg4 = await ctx.send("Você demorou muito para banir, tente novamente!")
            await asyncio.sleep(5)
            await msg4.delete()
```

# Agora vamos fazer avisar que o comando foi carregado sem nenhum erro :3

```Python
def setup(client):
  print("[Comando ban] Carregado.")
  client.add_cog(ban(client))
```
# Final:

```Python
import discord
import asyncio
from discord.ext import commands

class ban():
    def __init__(self, client):
        self.client = client
    @commands.command()
    async def ban(self,ctx,member: discord.Member=None):
        if ctx.author.guild_permissions.administrator:
            if member is None:
                await ctx.send(f"Olá {ctx.author.mention} você não marcou um user para banir")
        else:
            await ctx.send("Bobinhuh.. Você não tem permissão!")
        embed = discord.Embed(colour=0xff5d00)
        embed.set_author(name=f"Você deseja banir o {member.name}? (60 segundos)")
        embed.add_field(name="🆔ID:",value=member.id,inline=False)
        embed.add_field(name="📶Menção:",value=member.mention,inline=False)
        embed.add_field(name="🔢Tag:",value=member.discriminator,inline=False)
        embed.add_field(name="📆Criação da Conta:",value=member.created_at.strftime("**%H:%M:%S - %d/%m/20%y**"),inline=False)
        embed.add_field(name="☑️Entrada no Servidor:",value=member.joined_at.strftime("**%H:%M:%S - %d/%m/20%y**"),inline=False)
        embed.add_field(name="📱Atividade:",value=member.activity)
        embed.add_field(name="📷Avatar Link:",value="[Link Direto](" + member.avatar_url + ")\n",inline=False)
        embed.set_thumbnail(url=member.avatar_url)
        msg = await ctx.send(embed=embed)
        await msg.add_reaction("✅")
        await msg.add_reaction("❌")
        def check(reaction, user):
            return user == ctx.author and str(reaction.emoji)
        try:
            reaction, user = await self.client.wait_for('reaction_add', timeout=60.0, check=check)
            if reaction.emoji == "✅":
                await member.ban()
                await msg.delete()
                await ctx.send(f"Olá {ctx.author.mention} o {member.name} foi banido com sucesso")
            if reaction.emoji == "❌":
                await msg.delete()
        except asyncio.TimeoutError:
            await msg.delete()
            msg4 = await ctx.send("Você demorou muito para banir, tente novamente!")
            await asyncio.sleep(5)
            await msg4.delete()
def setup(client):
  print("[Comando ban] Carregado.")
  client.add_cog(ban(client))
```
