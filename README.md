# 🏘️ Idealista Bulk Property Scraper

Extract high-quality real estate data from **multiple Idealista property listings** across **Spain**, **Portugal**, and **Italy** in a single run.

This actor is designed for bulk property data extraction, processing search result pages and individual property listings efficiently. Perfect for real estate analysts, investors, agencies, and developers who need to scrape dozens or hundreds of properties at once.

---

## 🔎 What This Actor Does

This bulk scraper processes **Idealista search result pages** and extracts detailed information from each property listing, including:

* 📌 Title, description, and address
* 💰 Price information
* 📏 Area, number of rooms and bathrooms
* 🖼️ Complete image galleries
* 🏢 Agency details and contact information
* 📍 GPS coordinates and maps
* 🔧 Property features (terrace, elevator, AC, etc.)
* ⚡ Energy performance ratings
* 🏗️ Building characteristics

**Key Features:**
- **Bulk Processing**: Handle multiple search URLs simultaneously
- **Unlimited Extraction**: Bypass Idealista's 1,800-property pagination limit
- **Resume Capability**: Automatically resumes from where it left off if interrupted
- **Rate Limiting**: Built-in delays to respect server resources
- **Error Handling**: Robust retry mechanisms for failed requests

---

## 🛠️ How It Works

This actor uses the **[Idealista Scraper API](https://apify.com/dz_omar/idealista-scraper-api)** internally to extract individual property data. While the API actor processes one property at a time, this bulk scraper:

1. **Processes search URLs** containing multiple property listings
2. **Navigates through properties** automatically using smart navigation
3. **Calls the single-property API** for detailed data extraction
4. **Aggregates results** into a comprehensive dataset

> 💡 **Cost Efficiency**: Instead of manually running the single-property scraper hundreds of times, this actor automates the entire workflow.

---

## 🌐 Supported Input URLs

You can use this actor with **Idealista search result URLs** such as:

* `https://www.idealista.com/en/geo/venta-obranueva/andalucia/con-2-dormitorios,3-dormitorios,4-dormitorios/pagina-4?ordenado-por=precios-asc`
* `https://www.idealista.pt/comprar-casas/porto/`
* `https://www.idealista.it/vendita-case/roma/`

The actor will automatically detect the first property on the page and navigate through subsequent listings.

---

## ⚙️ Input Configuration

```json
{
  "Url": [
    "https://www.idealista.com/en/geo/venta-obranueva/andalucia/con-2-dormitorios,3-dormitorios,4-dormitorios/pagina-4?ordenado-por=precios-asc"
  ],
  "desiredResults": 50,
  "delayBetweenRequests": 600,
  "maxRetries": 3,
  "retryDelay": 600,
  "proxyConfig": {
    "useApifyProxy": true,
    "apifyProxyGroups": ["RESIDENTIAL"]
  }
}
```

### Input Parameters

| Parameter | Type | Description | Default |
|-----------|------|-------------|---------|
| `Url` | Array | List of Idealista search URLs to scrape | Required |
| `desiredResults` | Integer | Maximum properties to scrape (0 = no limit) | 1 |
| `delayBetweenRequests` | Integer | Delay between requests (100-2000ms) | 200 |
| `maxRetries` | Integer | Retry attempts for failed requests (0-5) | 3 |
| `retryDelay` | Integer | Initial retry delay (100-2000ms) | 200 |
| `proxyConfig` | Object | Proxy configuration (required) | RESIDENTIAL |

---

## 📊 Sample Output

Each property in your dataset will contain comprehensive information:

```json
{
  "id": "33826216",
  "Url": "https://www.idealista.pt/en/imovel/33826216/",
  "title": "T2 flat for sale in Ponta Delgada (Santa Clara)",
  "price": "399,950 €",
  "description": "Come and discover this amazing apartment located in the heart of Ponta Delgada...",
  "location": "Ponta Delgada",
  "characteristics": [
    "239 m² built, 217 m² floor area",
    "T2",
    "2 bathrooms",
    "Terrace"
  ],
  "building": ["With lift"],
  "amenities": ["Air conditioning"],
  "propertySpecs": {
    "rooms": 2,
    "bathrooms": 2,
    "garden": false,
    "pool": false,
    "terrace": true,
    "constructedArea": 239
  },
  "contactInfo": {
    "agency": "Comprarcasa Ponta Delgada",
    "phones": "+351 296 091 683",
    "reference": "326/A/03635"
  },
  "gallery": [
    {
      "url": "https://img4.idealista.pt/blur/WEB_DETAIL/0/id.pro.pt.image.master/20/ea/c7/267138555.jpg",
      "tag": "Views",
      "isPlan": false
    }
  ],
  "Map": {
    "src": "https://maps.googleapis.com/maps/api/staticmap?size=720x492&center=37.74504040%2C-25.69283370...",
    "addressVisibility": "HIDDEN"
  },
  "scrapedAt": "2025-05-27T01:04:23.968Z",
  "status": "success"
}
```

---

## 💰 New Pricing Model - Monthly Subscription + API Costs

**🎯 Monthly Subscription: $4.99/month + API costs per property**

This actor operates with a **monthly rental subscription** plus charges for the internal Idealista Scraper API calls. Here's the complete pricing breakdown:

### **Pricing Structure:**
- **Monthly Rental**: $4.99/month (auto-renewing subscription)
- **API Costs**: $0.003 per property (for internal Idealista Scraper API calls)
- **3-Day Free Trial**: Test the actor before committing to subscription

### **Cost Breakdown Per Property:**
**Idealista Scraper API Costs** (called internally for each property):
- **Actor Initialization**: $0.001 (per property extraction)
- **Property Data Extracted**: $0.002 (per successful property)
- **Total API Cost**: $0.003 per property

### **Total Monthly Cost Examples:**

| Properties | Monthly Subscription | API Costs | Total Monthly Cost |
|------------|---------------------|-----------|-------------------|
| 1 property | $4.99 | 1 × $0.003 = $0.003 | **$4.993** |
| 10 properties | $4.99 | 10 × $0.003 = $0.03 | **$5.02** |
| 100 properties | $4.99 | 100 × $0.003 = $0.30 | **$5.29** |
| 500 properties | $4.99 | 500 × $0.003 = $1.50 | **$6.49** |
| 1,000 properties | $4.99 | 1,000 × $0.003 = $3.00 | **$7.99** |
| 2,000 properties | $4.99 | 2,000 × $0.003 = $6.00 | **$10.99** |
| 5,000 properties | $4.99 | 5,000 × $0.003 = $15.00 | **$19.99** |
| 10,000 properties | $4.99 | 10,000 × $0.003 = $30.00 | **$34.99** |

### **Cost Formula:**
```
Monthly Total = $4.99 + (Number of Properties × $0.003)
```

### **Additional Platform Costs:**
You'll still pay standard Apify platform costs for:
- **Compute Units**: For running the actor
- **Storage**: For storing extracted data
- **Residential Proxies**: Already included in Apify proxy costs

---

## 🚀 Use Cases

* **🏢 Real Estate Agencies**: Bulk market analysis and competitor research
* **📈 Property Investors**: Track market trends across multiple regions
* **🔍 SEO & Content Teams**: Gather property data for content creation
* **🤖 Developers**: Build automated property monitoring systems
* **📊 Market Analysts**: Extract insights from large property datasets
* **🏗️ Construction Companies**: Identify development opportunities

---

## ⚡ Key Features

### **Unlimited Extraction Capability**
- **Breaks Through Idealista's 60-Page Limit**: While Idealista typically limits users to 60 pages (≈1,800 properties) and shows the message *"Have you seen 1,800 homes and still can't find what you're looking for?"*, this actor can extract **ALL available properties**
- **No Artificial Limits**: Extract thousands of properties from a single search URL
- **Continuous Navigation**: Uses internal property navigation to bypass page limitations
- **Only Limited by Your Subscription**: Extract properties with active subscription (API costs apply per property)

> 🚀 **Breakthrough Feature**: Most scrapers hit Idealista's 1,800-property wall, but this actor navigates property-by-property, completely bypassing pagination limits!

### **Resume Capability**
- Automatically saves progress during execution
- Resumes from the last processed property if interrupted
- Perfect for large-scale scraping operations

### **Smart Error Handling**
- Exponential backoff for failed requests
- Skips invalid properties automatically
- Comprehensive logging for debugging

### **Rate Limiting**
- Configurable delays between requests
- Respects server resources
- Reduces risk of being blocked

### **Multi-Domain Support**
- Spain: `idealista.com`
- Portugal: `idealista.pt`
- Italy: `idealista.it`

---

## 📚 Technical Requirements

### **Proxy Configuration**
Residential proxies are **required** for reliable operation:

```json
"proxyConfig": {
  "useApifyProxy": true,
  "apifyProxyGroups": ["RESIDENTIAL"]
}
```

### **Input Validation**
- Only Idealista domains are accepted
- URLs must be properly formatted search result pages
- Invalid URLs are automatically skipped

---

## ⚖️ Legal & Ethical Considerations

This actor:
- ✅ Respects `robots.txt` directives
- ✅ Implements appropriate rate limiting
- ✅ Only extracts publicly available data
- ✅ Does not bypass paywalls or authentication

---

## 🔧 Advanced Configuration

### **For Unlimited Large-Scale Extraction**
```json
{
  "desiredResults": 0,
  "delayBetweenRequests": 1000,
  "maxRetries": 5,
  "retryDelay": 1000
}
```
> 💡 Set `desiredResults: 0` to extract ALL properties available, breaking through Idealista's typical 1,800-property limit.

### **For Quick Testing**
```json
{
  "desiredResults": 10,
  "delayBetweenRequests": 500,
  "maxRetries": 2,
  "retryDelay": 500
}
```

### **Important Notes for Large Extractions:**
- **Subscription Required**: Active $4.99/month subscription needed
- **Platform Costs**: Additional platform usage costs apply
- **Time Investment**: Extracting 10,000 properties may take several hours due to rate limiting
- **Monitor Progress**: Use Apify's dashboard to track extraction progress
- **Resume Feature**: If interrupted, the actor will automatically continue from the last processed property

---

## 🎯 Getting Started

1. **Start Free Trial**: Activate the 3-day free trial
2. **Test the Actor**: Run small extractions to verify functionality
3. **Subscribe**: Convert to monthly subscription for unlimited access
4. **Scale Up**: Extract thousands of properties with confidence

### **Subscription Management**
- **Auto-Renewal**: Monthly subscription automatically renews
- **Cancel Anytime**: Cancel subscription in Apify Console
- **Immediate Access**: Start extracting immediately after subscription

---

## 🤝 Support & Contact

For assistance, custom implementations, or bulk processing needs:

* 📧 Email: [fridaytechnolog@gmail.com](mailto:fridaytechnolog@gmail.com)
* 🐙 GitHub: [DZ-ABDLHAKIM](https://github.com/DZ-ABDLHAKIM)
* 🐦 Twitter: [@DZ_45Omar](https://x.com/DZ_45Omar)
* 🔧 Apify: [dz_omar](https://apify.com/dz_omar)

---

## 📝 Version History

- **v2.0**: New pay-per-event pricing model with monthly subscription
- **v1.0**: Initial release with bulk scraping capabilities
- Built on top of the proven [Idealista Scraper API](https://apify.com/dz_omar/idealista-scraper-api)

---
