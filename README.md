# Loot Radar

Find the biggest discounts in your local Swiggy Instamart store.

There are two parts:

- **Bookmarklet**: a bookmark you click while on Instamart. Pick some aisles and you get a list of the best deals.
- **Deal alert bot**: runs on GitHub Actions and sends new deals to Telegram every 30 minutes.

## Bookmarklet

Open **https://stymrj.github.io/swiggy-instamart-deals-tracker/** and follow the steps there.

- **Computer:** drag the **Loot Radar** button to your bookmarks bar, open swiggy.com/instamart and click it.
- **Phone:** tap **Copy code**, bookmark any page, then edit the bookmark: name it `Loot Radar` and paste the code as the URL. On Instamart, type `Loot Radar` in the address bar and tap it.

Set your delivery address on Instamart first so it picks up the right store.

## Deal alert bot

1. **Fork** this repo.
2. **Create a Telegram bot** with [@BotFather](https://t.me/BotFather) and note the token. Get your chat ID from [@userinfobot](https://t.me/userinfobot).
3. **Find your store ID.** Open any category on Instamart and copy `storeId` (and `secondaryStoreId` if there is one) from the URL.
4. **Add secrets** under *Settings → Secrets and variables → Actions*:

   | Secret | Required |
   | --- | --- |
   | `TELEGRAM_BOT_TOKEN` | yes |
   | `TELEGRAM_CHAT_ID` | yes |
   | `SWIGGY_STORE_ID` | yes |
   | `SWIGGY_PRIMARY_STORE_ID` | yes (same as store ID) |
   | `SWIGGY_SECONDARY_STORE_ID` | no |

5. **Turn on Actions** in your fork, open **Instamart Deal Alerts** and click **Run workflow**.

After that it runs every 30 minutes from 9 AM to midnight IST. It only sends new deals, price drops and items back in stock, so you won't get repeats.

### Discount thresholds

Each group has its own minimum discount. You can change them with these optional secrets:

| Group | Secret | Default |
| --- | --- | --- |
| Fresh produce & meat | `FRESH_MIN_DISCOUNT` | 60 |
| Staples & cooking | `GROCERY_MIN_DISCOUNT` | 60 |
| Sweets & chocolates | `TREATS_MIN_DISCOUNT` | 70 |
| Snacks & instant food | `MUNCHIES_MIN_DISCOUNT` | 70 |
| Drinks & breakfast | `BEVERAGES_MIN_DISCOUNT` | 70 |
| Personal care | `PERSONAL_MIN_DISCOUNT` | 70 |
| Baby & home | `LIFESTYLE_MIN_DISCOUNT` | 85 |

Aisles for each group are listed in `deal-alert-bot/config.json`.

## Run locally

```bash
cd deal-alert-bot
npm install
cp .env.example .env   # fill in your token, chat ID and store ID
npm run test:grocery   # or test:fresh, test:treats, ...
npm start              # interactive Telegram bot
```

## Files

```
index.html                   setup page
loot-radar.js                bookmarklet source
loot-radar.min.js            minified bookmarklet
loot-radar.bookmarklet.txt   offline bookmarklet
deal-alert-bot/              Telegram bot
.github/workflows/           scheduled runs
```

---

Made with ❤️ by Satyam Raj · Based on [jairaj26/swiggy-instamart-deals](https://github.com/jairaj26/swiggy-instamart-deals) · Not affiliated with Swiggy.
