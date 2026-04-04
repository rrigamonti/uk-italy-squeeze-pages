# Campaign Tracking Setup Guide
## UK/Italy E-commerce Launch

### Overview
This guide provides step‑by‑step instructions to implement tracking for both UK and Italian squeeze page campaigns. Proper tracking is essential to measure conversion rates, ROI, and campaign effectiveness.

---

## 1. Google Analytics 4 (GA4)
### Setup Steps
1. **Create GA4 Property** (if not already done)
   - Go to [analytics.google.com](https://analytics.google.com)
   - Admin → Create Property → "UK/Italy Squeeze Campaigns"
   - Data stream → Web → Enter squeeze page URLs:
     - UK: `https://your‑domain.com/squeeze‑page‑uk.html`
     - Italy: `https://your‑domain.com/squeeze‑page‑italy.html`

2. **Install GA4 Snippet**  
   Add the following code **just before `</head>`** in both HTML files:
   ```html
   <!-- Google tag (gtag.js) -->
   <script async src="https://www.googletagmanager.com/gtag/js?id=G-XXXXXXXXXX"></script>
   <script>
     window.dataLayer = window.dataLayer || [];
     function gtag(){dataLayer.push(arguments);}
     gtag('js', new Date());
     gtag('config', 'G-XXXXXXXXXX');
   </script>
   ```
   Replace `G-XXXXXXXXXX` with your actual Measurement ID.

3. **Configure Events**  
   Track these key events:
   - `page_view` (automatic)
   - `email_submit` (when form is submitted)
   - `download_click` (when "Download Free Blueprint" is clicked)

   **Example event code for email submission:**
   ```javascript
   document.querySelector('form').addEventListener('submit', function() {
     gtag('event', 'email_submit', {
       'campaign_name': 'UK_Ecommerce_Blueprint',
       'form_location': 'hero_section'
     });
   });
   ```

---

## 2. Facebook/Meta Pixel
### Setup Steps
1. **Create Meta Pixel**
   - Go to [Meta Events Manager](https://business.facebook.com/events_manager)
   - Create Pixel → Name: "UK‑Italy Squeeze Pixel"
   - Copy the base pixel code.

2. **Install Pixel Code**  
   Insert the code **just after `<head>`** in both HTML files:
   ```html
   <!-- Meta Pixel Code -->
   <script>
   !function(f,b,e,v,n,t,s)
   {if(f.fbq)return;n=f.fbq=function(){n.callMethod?
   n.callMethod.apply(n,arguments):n.queue.push(arguments)};
   if(!f._fbq)f._fbq=n;n.push=n;n.loaded=!0;n.version='2.0';
   n.queue=[];t=b.createElement(e);t.async=!0;
   t.src=v;s=b.getElementsByTagName(e)[0];
   s.parentNode.insertBefore(t,s)}(window, document,'script',
   'https://connect.facebook.net/en_US/fbevents.js');
   fbq('init', 'YOUR_PIXEL_ID');
   fbq('track', 'PageView');
   </script>
   <noscript><img height="1" width="1" style="display:none"
   src="https://www.facebook.com/tr?id=YOUR_PIXEL_ID&ev=PageView&noscript=1"
   /></noscript>
   <!-- End Meta Pixel Code -->
   ```

3. **Track Conversions**  
   Add event tracking for form submissions:
   ```javascript
   document.querySelector('form').addEventListener('submit', function() {
     fbq('track', 'Lead', {
       content_name: 'UK_Ecommerce_Blueprint',
       content_category: 'Free_Download'
     });
   });
   ```

---

## 3. UTM Parameters
### URL Structure
Use these UTM parameters in all campaign links:

**UK Campaign:**
```
https://your‑domain.com/squeeze‑page‑uk.html
?utm_source=facebook
&utm_medium=paid
&utm_campaign=uk_ecommerce_blueprint_2026
&utm_content=video_ad
&utm_term=business_owners_2M‑10M
```

**Italy Campaign:**
```
https://your‑domain.com/squeeze‑page‑italy.html
?utm_source=linkedin
&utm_medium=sponsored
&utm_campaign=italy_pmi_compliance_2026
&utm_content=carousel_ad
&utm_term=pm_15‑250_dipendenti
```

### Recommended Values
| Parameter | UK Value | Italy Value | Purpose |
|-----------|----------|-------------|---------|
| `utm_source` | `facebook`, `google`, `linkedin`, `email` | `linkedin`, `facebook`, `google` | Traffic source |
| `utm_medium` | `paid`, `cpc`, `social`, `email` | `sponsored`, `cpc`, `social` | Medium type |
| `utm_campaign` | `uk_ecommerce_blueprint_2026` | `italy_pmi_compliance_2026` | Campaign name |
| `utm_content` | `video_ad`, `image_ad`, `lead_form` | `carousel_ad`, `document_ad` | Ad creative |
| `utm_term` | `business_owners_2M‑10M`, `post‑brexit` | `pm_15‑250_dipendenti`, `ateco_2026` | Targeting keywords |

---

## 4. Email Service Integration
### Mailchimp / ActiveCampaign / ConvertKit
1. **Create a landing‑page form** in your email service.
2. **Embed the form code** in your HTML files (replace the existing `<form>`).
3. **Set up automation**:
   - Trigger: Form submission
   - Action: Send "Blueprint Download" email with PDF link
   - Follow‑up: 7‑email sequence (already drafted)

**Example Mailchimp embed:**
```html
<!-- Begin Mailchimp Signup Form -->
<div id="mc_embed_signup">
  <form action="https://your‑domain.us21.list‑manage.com/subscribe/post" method="post" id="mc‑embedded‑subscribe‑form" name="mc‑embedded‑subscribe‑form" class="validate" target="_blank" novalidate>
    <input type="email" value="" name="EMAIL" class="email" id="mce‑EMAIL" placeholder="Enter your email" required>
    <div style="position: absolute; left: ‑5000px;" aria‑hidden="true"><input type="text" name="b_xxxxxxxxxxxxxxxxxxxxxx" tabindex="‑1" value=""></div>
    <button type="submit" name="subscribe" id="mc‑embedded‑subscribe">Download Free Blueprint</button>
  </form>
</div>
<!-- End Mailchimp Signup Form -->
```

---

## 5. Conversion Tracking Dashboard
### Recommended Metrics
| Metric | Target (UK) | Target (Italy) | Tool |
|--------|-------------|----------------|------|
| Conversion Rate | ≥ 25% | ≥ 20% | GA4 |
| Cost per Lead (CPL) | ≤ £15 | ≤ €12 | Meta Ads Manager |
| Email Open Rate | ≥ 45% | ≥ 40% | Email Service |
| PDF Download Rate | ≥ 90% of leads | ≥ 85% of leads | GA4 Events |
| 7‑day Retention | ≥ 60% | ≥ 55% | Email Service |

### Dashboard Setup
1. **Google Data Studio / Looker Studio**
   - Connect GA4, Facebook Ads, Email Service data sources
   - Create a dashboard with:
     - Daily leads & conversion rate
     - Campaign‑wise performance
     - ROI calculation (lead value vs. ad spend)

2. **Weekly Review Checklist**
   - Check tracking codes are firing (use Google Tag Assistant)
   - Verify UTM parameters are correctly appended
   - Review conversion rates per traffic source
   - Adjust bids/targeting based on CPL

---

## 6. Troubleshooting
### Common Issues
| Issue | Solution |
|-------|----------|
| GA4 events not showing | Check Measurement ID, enable debug mode |
| Facebook Pixel not firing | Use Facebook Pixel Helper extension |
| Form submissions not tracked | Verify JavaScript event listeners are attached |
| UTM parameters lost | Ensure links preserve query strings |

### Validation Tools
- **Google Tag Assistant** (Chrome extension)
- **Facebook Pixel Helper** (Chrome extension)
- **UTM Builder** (https://ga-dev‑tools.web.app/campaign‑url‑builder/)

---

## Next Steps
1. **Implement GA4 & Meta Pixel** codes in both HTML files.
2. **Update all campaign links** with proper UTM parameters.
3. **Test** using validation tools.
4. **Monitor** dashboard daily for first week.
5. **Optimize** based on conversion data.

---

**Last Updated:** 2026‑04‑02  
**Contact:** info@rrigamonti.com  
**Project:** UK/Italy E‑commerce Launch Phase 3