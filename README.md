# Bettlgraund- import random
import time

# --- Game Data ---
player_data = {
    "diamonds": 0,
    "coins": 1000,
    "level": 1,
    "rank": "Bronze I",
    "inventory": []
}

# --- 1. Pro Matchmaking & Headshot Logic ---
def play_match(mode):
    print(f"\n--- ⚔️ Match Started: {mode} (Ranked) ---")
    print("🤖 Pro Bots are spawning... Watch out for Headshots!")
    time.sleep(2)
    
    # Skill based result
    kills = random.randint(2, 12)
    is_booyah = random.choice([True, False])
    
    if is_booyah:
        print(f"🏆 BOOYAH! Kills: {kills}")
        player_data["diamonds"] += 499
        player_data["level"] += 5
        print("💎 Reward: +499 Diamonds added!")
    else:
        print(f"💀 Eliminated! Kills: {kills}. Try again for Booyah.")
        player_data["level"] += 1

    check_level_rewards()
    update_rank()

# --- 2. Level Rewards (Criminal & Sakura) ---
def check_level_rewards():
    lvl = player_data["level"]
    if lvl >= 50 and "Red Criminal" not in player_data["inventory"]:
        player_data["inventory"].append("Red Criminal")
        print("🎁 LEVEL 50 REACHED! Red Criminal Bundle Unlocked! 🔥")
    if lvl >= 60 and "Sakura Bundle" not in player_data["inventory"]:
        player_data["inventory"].append("Sakura Bundle")
        print("🌸 LEVEL 60 REACHED! Legendary Sakura Bundle Unlocked! 🌸")

# --- 3. Rank System (Grandmaster tak) ---
def update_rank():
    lvl = player_data["level"]
    if lvl < 20: player_data["rank"] = "Silver"
    elif lvl < 50: player_data["rank"] = "Gold"
    elif lvl < 100: player_data["rank"] = "Heroic"
    else: player_data["rank"] = "✨ GRANDMASTER ✨"

# --- 4. Luck Royale (50 Spins Guarantee) ---
luck_points = 0
def spin_royale():
    global luck_points
    if player_data["coins"] < 500:
        print("❌ Coins kam hain! Match khelo.")
        return

    player_data["coins"] -= 500
    luck_points += 1
    print(f"🎰 Spinning... Luck: {luck_points}/50")

    if luck_points >= 50 or random.randint(1, 100) <= 5:
        item = random.choice(["Hip Hop Bundle", "Cobra MP40", "Flag Emote"])
        player_data["inventory"].append(item)
        print(f"🎊 CONGRATULATIONS! You got: {item}")
        luck_points = 0
    else:
        print("☁️ Better luck next time!")

# --- Main Menu Loop ---
def game_loop():
    while True:
        print(f"\n--- 🏠 MAIN MENU | Level: {player_data['level']} | Rank: {player_data['rank']} ---")
        print(f"💎 Diamonds: {player_data['diamonds']} | 🪙 Coins: {player_data['coins']}")
        print("1. Play CS Rank (4vs4)")
        print("2. Play BR Rank")
        print("3. Luck Royale (Spin)")
        print("4. Check Inventory")
        print("5. Exit")
        
        choice = input("Select Option: ")
        if choice == "1" or choice == "2":
            play_match("CS" if choice == "1" else "BR")
        elif choice == "3":
            spin_royale()
        elif choice == "4":
            print(f"📦 Your Items: {player_data['inventory']}")
        elif choice == "5":
            break

game_loop()
