# Elysium - Gelişmiş Discord Botu

Discord botu için komutlar.

## Slash Commands

- `/çark` - Çark çevir ve şanslı sayı kazanı! 🎡
- `/ark` - Ark çevir ve 1-10 arasında sayı kazanı! 🎲

## Kurulum

```bash
pip install discord.py
```

## Bot Kodu

```python
import discord
from discord.ext import commands
from discord import app_commands
import asyncio
import random

# Bot intenti ayarla
intents = discord.Intents.default()
intents.message_content = True

bot = commands.Bot(command_prefix=".", intents=intents)

@bot.event
async def on_ready():
    await bot.tree.sync()
    print(f'{bot.user} olarak giriş yapıldı')

@app_commands.command(name="çark", description="Çark çevir ve şanslı sayı kazanı! 🎡")
async def cark_slash(interaction: discord.Interaction):
    await interaction.response.defer()
    
    embed_rolling = discord.Embed(title="🎡 Çark Döndürülüyor...", description="Şanslı sayı seçiliyor, lütfen bekleyin...", color=discord.Color.blue())
    await interaction.followup.send(embed=embed_rolling)
    await asyncio.sleep(2)

    sayi_havuzu = []
    for i in range(1, 11):
        if i in [1, 6]: 
            sayi_havuzu.append(i)
        else: 
            sayi_havuzu.extend([i] * 10)

    sansli_sayi = random.choice(sayi_havuzu)
    embed_result = discord.Embed(title="🎡 Çark Döndü! 🎉", description=f"🔮 Şansına Gelen Sayı:\n\n# **{sansli_sayi}**\n\n*İyi şanslar dileriz!*", color=discord.Color.green())
    await interaction.followup.send(embed=embed_result)

@app_commands.command(name="ark", description="Ark çevir ve 1-10 arasında sayı kazanı! 🎲")
async def ark_slash(interaction: discord.Interaction):
    await interaction.response.defer()
    
    embed_rolling = discord.Embed(title="🎡 Çark Döndürülüyor...", description="Sayı seçiliyor, lütfen bekleyin...", color=discord.Color.blue())
    await interaction.followup.send(embed=embed_rolling)
    await asyncio.sleep(2)
    
    sayi_havuzu = []
    for i in range(1, 11):
        if i == 3:
            sayi_havuzu.append(i)
        else:
            sayi_havuzu.extend([i] * 10)
    
    sansli_sayi = random.choice(sayi_havuzu)
    embed_result = discord.Embed(title="🎡 Çark Döndü! 🎉", description=f"🔮 Şansına Gelen Sayı:\n\n# **{sansli_sayi}**\n\n*İyi şanslar dileriz!*", color=discord.Color.green())
    await interaction.followup.send(embed=embed_result)

bot.tree.add_command(cark_slash)
bot.tree.add_command(ark_slash)

bot.run('YOUR_BOT_TOKEN')
```

## Başlatma

```bash
python bot.py
```
