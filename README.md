
@bot.command(name="cark")
async def cark_cmd1(ctx):
    await perform_cark(ctx)

@bot.command(name="çark")
async def cark_cmd2(ctx):
    await perform_cark(ctx)

async def perform_cark(ctx):
    embed_rolling = discord.Embed(title="🎡 Çark Döndürülüyor...", description="Şanslı sayı seçiliyor, lütfen bekleyin...", color=discord.Color.blue())
    roll_msg = await ctx.send(embed=embed_rolling)
    await asyncio.sleep(2)

    # 1 ve 6 sayılarından havuza sadece 1'er adet eklenirken, 
    # diğer sayıların her birinden 10'ar adet eklenerek gelme ihtimalleri düşürülüyor.
    sayi_havuzu = []
    for i in range(1, 11):
        if i in [1, 6]: 
            sayi_havuzu.append(i)
        else: 
            sayi_havuzu.extend([i] * 10)

    sansli_sayi = random.choice(sayi_havuzu)
    embed_result = discord.Embed(title="🎡 Çark Döndü! 🎉", description=f"🔮 Şansına Gelen Sayı:\n\n# **{sansli_sayi}**\n\n*İyi şanslar dileriz!*", color=discord.Color.green())
    await roll_msg.edit(embed=embed_result)
