# WNC Pay — Web Developer Guide / מדריך למפתח האתר

**English first, עברית למטה.**

---

## English

### What is installed on the site

The **WNC Pay** plugin (currently v0.4.0) connects israel-extreme.com to the operator's payment & booking platform. It provides two things:

1. **Embeds** — the gift-card designer (and future elements) placed anywhere on the site.
2. **A WooCommerce payment gateway** — checkout redirects to the platform's secure payment page; the order is completed automatically by a signed webhook from the platform.

The plugin **updates itself** through WordPress's normal update system (from this repository). **Never edit the plugin's code** — changes are overwritten on the next update. Configuration lives in **Settings → WNC Pay** (connection) and **WooCommerce → Settings → Payments → WNC Pay** (gateway options).

### Your checklist

1. **Keep the plugin updated.** Updates appear on the Plugins screen like any other plugin. Install them.
2. **WP Rocket** (or any JS-delay optimizer): keep the keyword `wncpay` in *Delay JavaScript execution → Excluded JavaScript files*. Without it, embeds keep their fallback height until the visitor interacts.
3. **Create the gift page (this is yours to do — no page exists yet).** Update the existing "Gift Certificates" page (or create a new one, your call) to host the designer: drop in the **Gift Card Designer** Elementor widget ("WNC Pay" category) or the shortcode `[wncpay_gift_designer]`. Create the Hebrew version via WPML as usual — the embed follows the page language automatically. Then point every gift button/tile/menu entry at that page. The element resizes itself; give it room (a full-width section works best).
4. **Mark instant products.** Open each product that is **NOT a tour requiring availability confirmation** (merchandise, instantly-confirmable items) and tick **"WNC Pay: full payment"** in the product data (General tab). Flagged products charge 100% immediately and skip the date question. **Unflagged products are treated as tours**: checkout asks the customer's preferred date (required), charges a deposit (configurable, default 30%), and the office confirms availability before the balance.
5. **Gift cards are NOT WooCommerce products.** Do not create a Woo gift-card product. All gift buttons/tiles must link to the gift page that hosts the designer embed (see below). The legacy PW WooCommerce Gift Cards and Z-Credit plugins are being retired — coordinate before touching them.
6. **Placing the gift designer**: use the **Elementor widget** ("WNC Pay" category → Gift Card Designer), the shortcode `[wncpay_gift_designer]`, or the Gutenberg block. The full attribute reference (amount, matchkey, product, dealid, prefills, min_height…) is on **Settings → WNC Pay**. The embed follows the page language (WPML) automatically.
7. **Enabling the gateway**: WooCommerce → Settings → Payments → **WNC Pay** → Enable — only when the site owner says go. Before enabling, confirm Settings → WNC Pay shows **"✓ Connected"**. Do not enable any other payment gateway alongside it without coordination — there is one money path.
8. **Currency must stay ILS.** The gateway only offers itself for ILS carts.
9. **Staging**: if you test on a staging domain, send the exact staging origin to the site owner so it can be whitelisted for embeds (they will not render on unlisted domains — that is by design, not a bug).

### How a paid order behaves

- Full payment → order goes to **Processing** automatically, with the platform reference in the order notes.
- Deposit (tour) orders → order sits **On hold** with a note ("deposit received — awaiting office availability confirmation"). When the office confirms and charges the balance **on the platform**, the order completes by itself. This is normal — do not "fix" on-hold orders.
- Customers see a link to their platform account (receipts, balance, documents) on the thank-you page and in order emails.

### Support boundary

The plugin's job ends at rendering embeds and handing checkout to the platform. **Styling and placement** of elements: you. **Everything inside the frames and the payment flow** (designs, checkout, receipts, documents): the platform operator. If an embed shows nothing: check the Settings page connection indicator first, then the browser console, then contact the operator.

---


### New in 0.5.0–0.6.0 (2026-08-04)

- **Test mode** (gateway setting, WooCommerce → Settings → Payments → WNC Pay): checkouts run against the PayMe sandbox — the PayMe test card is approved for real, no actual money moves, and the platform stamps everything [TEST]. A yellow TEST banner shows at checkout while enabled. Use it to validate the full flow end-to-end, then turn it OFF before go-live.
- **Two new embeds** (Elementor "WNC Pay" category or shortcodes): `[wncpay_trip_planner]` — the interactive trip-builder wizard; `[wncpay_tour_catalog]` — browse and pick multiple tours in one place. Use these instead of linking visitors off-site: point the site's "Build your itinerary" button at a page hosting `[wncpay_trip_planner]`, and "Get more info" buttons at a page hosting `[wncpay_tour_catalog]`.
- **Cross-site failover** (automatic, nothing to configure): if a browser privacy setting or blocker prevents an embed from loading, it replaces itself with an "Open it in a new tab" card instead of a blank frame.

## עברית

### מה מותקן באתר

תוסף **WNC Pay** (כרגע v0.4.0) מחבר את israel-extreme.com לפלטפורמת התשלומים וההזמנות של המפעיל. הוא מספק שני דברים:

1. **Embeds** — מעצב שוברי המתנה (ואלמנטים עתידיים) בכל מקום באתר.
2. **שער תשלום (gateway) ל-WooCommerce** — ה-checkout מפנה לעמוד תשלום מאובטח בפלטפורמה; ההזמנה נסגרת אוטומטית ע"י webhook חתום מהפלטפורמה.

התוסף **מתעדכן לבד** דרך מערכת העדכונים הרגילה של וורדפרס (מהריפוזיטורי הזה). **אין לערוך את קוד התוסף** — שינויים יידרסו בעדכון הבא. ההגדרות נמצאות ב-**Settings → WNC Pay** (חיבור) וב-**WooCommerce → Settings → Payments → WNC Pay** (אפשרויות השער).

### הצ'קליסט שלך

1. **לעדכן את התוסף.** עדכונים מופיעים במסך התוספים כרגיל — יש להתקין אותם.
2. **WP Rocket** (או כל אופטימיזציית delay ל-JS): להשאיר את מילת המפתח `wncpay` ב-*Delay JavaScript execution → Excluded JavaScript files*. בלעדיה ה-embeds יישארו בגובה ברירת המחדל עד אינטראקציה של המבקר.
3. **ליצור את עמוד המתנות (משימה שלכם — העמוד עדיין לא קיים).** עדכנו את עמוד "Gift Certificates" הקיים (או צרו עמוד חדש, לשיקולכם) כך שיארח את המעצב: הוסיפו את ווידג'ט **Gift Card Designer** ב-Elementor (קטגוריית "WNC Pay") או את ה-shortcode‏ `[wncpay_gift_designer]`. צרו את הגרסה בעברית דרך WPML כרגיל — ה-embed עוקב אחרי שפת העמוד אוטומטית. לאחר מכן כוונו לעמוד הזה כל כפתור/אריח/פריט תפריט של מתנות. האלמנט מתאים את גובהו לבד; תנו לו מקום (סקשן ברוחב מלא עובד הכי טוב).
4. **לסמן מוצרים מיידיים.** בכל מוצר ש**אינו טיול הדורש אישור זמינות** (מרצ'נדייז, פריטים מיידיים) יש לסמן **"WNC Pay: full payment"** בעריכת המוצר (לשונית General). מוצר מסומן נגבה 100% מיד וללא שאלת תאריך. **מוצר לא מסומן נחשב טיול**: ה-checkout שואל תאריך מועדף (חובה), גובה מקדמה (ברירת מחדל 30%), והמשרד מאשר זמינות לפני היתרה.
5. **שוברי מתנה אינם מוצרי WooCommerce.** אין ליצור מוצר שובר בווקומרס. כל כפתורי/אריחי המתנה מקשרים לעמוד המתנה שמארח את ה-embed של המעצב (ראו סעיף 5). התוספים הישנים PW Gift Cards ו-Z-Credit בתהליך הוצאה משימוש — לתאם לפני שנוגעים.
6. **הצבת מעצב השוברים**: דרך **ווידג'ט Elementor** (קטגוריית "WNC Pay" → Gift Card Designer), דרך shortcode‏ `[wncpay_gift_designer]`, או בלוק גוטנברג. טבלת כל הפרמטרים (amount, matchkey, product, dealid, prefills, min_height…) נמצאת ב-**Settings → WNC Pay**. ה-embed עוקב אוטומטית אחרי שפת העמוד (WPML).
7. **הפעלת השער**: WooCommerce → Settings → Payments → **WNC Pay** → Enable — רק כשבעל האתר מאשר. לפני ההפעלה לוודא ש-Settings → WNC Pay מציג **"✓ Connected"**. אין להפעיל שער תשלום נוסף לצידו ללא תיאום — יש מסלול כסף אחד.
8. **המטבע חייב להישאר ILS.** השער מציע את עצמו רק לעגלות בשקלים.
9. **Staging**: אם בודקים על דומיין staging, יש לשלוח לבעל האתר את ה-origin המדויק כדי להוסיף אותו לרשימת ההיתרים של ה-embeds (הם לא יוצגו על דומיין לא רשום — זו התנהגות מכוונת, לא באג).

### איך מתנהגת הזמנה ששולמה

- תשלום מלא → ההזמנה עוברת ל-**Processing** אוטומטית, עם ה-reference של הפלטפורמה בהערות ההזמנה.
- הזמנת מקדמה (טיול) → ההזמנה עומדת ב-**On hold** עם הערה ("deposit received — awaiting office availability confirmation"). כשהמשרד מאשר וגובה את היתרה **בפלטפורמה**, ההזמנה נסגרת מעצמה. זה תקין — אין "לתקן" הזמנות On hold.
- הלקוח מקבל קישור לחשבון שלו בפלטפורמה (קבלות, יתרה, מסמכים) בעמוד התודה ובמיילים של ההזמנה.

### גבולות אחריות

תפקיד התוסף מסתיים בהצגת ה-embeds ובהעברת ה-checkout לפלטפורמה. **עיצוב ומיקום** של האלמנטים: אתם. **כל מה שבתוך הפריימים וזרימת התשלום** (עיצובים, checkout, קבלות, מסמכים): מפעיל הפלטפורמה. אם embed לא מציג כלום: קודם בודקים את אינדיקטור החיבור בעמוד ההגדרות, אחר כך את קונסולת הדפדפן, ואז פונים למפעיל.

### חדש ב-0.5.0–0.6.0 (2026-08-04)

- **מצב בדיקה** (הגדרת שער התשלום): הזמנות רצות מול סביבת ה-Sandbox של PayMe — כרטיס הבדיקה מאושר באמת, שום כסף אמיתי לא זז, והפלטפורמה מסמנת הכול [TEST]. באנר צהוב מוצג בצ'קאאוט כשהמצב פעיל. השתמשו בו לבדיקת הזרימה מקצה לקצה, וכבו לפני עלייה לאוויר.
- **שני embeds חדשים** (ווידג'ט Elementor או shortcode): ‏`[wncpay_trip_planner]` — אשף בניית מסלול אינטראקטיבי; ‏`[wncpay_tour_catalog]` — קטלוג טיולים שבו הלקוח בוחר כמה פריטים במקום אחד. השתמשו בהם במקום להפנות מבקרים לאתר חיצוני: כפתור "Build your itinerary" מפנה לעמוד עם ה-planner, וכפתורי "Get more info" לעמוד עם הקטלוג.
- **Failover אוטומטי**: אם דפדפן חוסם את ה-embed, הוא מוחלף מעצמו בכרטיס "פתיחה בלשונית חדשה" במקום מסגרת ריקה. אין מה להגדיר.
