# GSON+ANDROID
How to download data using gson and store it in a android app

### json preview 

```
{  
   "result":true,
   "priceGroup":[  
      {  
         "priceG_Id":13368,
         "price_list_no":"BDGT",
         "priceG_Name":"BUDGET PRICE LIST",
         "items":[  
            {  
               "product_id":4042,
               "catalog_no":"30WLT120",
               "mrp":"3850.00",
               "sale_price":"2845.65"
            }
         ]
      }
   ]
}

```
Create classes those are matching with json

```
public class PriceGroupResponse {

    private String result;
    private ArrayList<PriceGroupG> priceGroup;


    public String getResult() {
        return result;
    }

    public void setResult(String result) {
        this.result = result;
    }

    public ArrayList<PriceGroupG> getPriceGroup() {
        return priceGroup;
    }

    public void setPriceGroup(ArrayList<PriceGroupG> priceGroup) {
        this.priceGroup = priceGroup;
    }
}

```

```
public class PriceGroupG {

    private String priceG_Id;
    private String price_list_no;
    private String priceG_Name;
    private ArrayList<PriceGroupItemG> items;


    public String getPriceG_Id() {
        return priceG_Id;
    }

    public void setPriceG_Id(String priceG_Id) {
        this.priceG_Id = priceG_Id;
    }

    public String getPrice_list_no() {
        return price_list_no;
    }

    public void setPrice_list_no(String price_list_no) {
        this.price_list_no = price_list_no;
    }

    public String getPriceG_Name() {
        return priceG_Name;
    }

    public void setPriceG_Name(String priceG_Name) {
        this.priceG_Name = priceG_Name;
    }

    public ArrayList<PriceGroupItemG> getItems() {
        return items;
    }

    public void setItems(ArrayList<PriceGroupItemG> items) {
        this.items = items;
    }
}

```

```
public class PriceGroupItemG {

    private String product_id;
    private String catalog_no;
    private String mrp;
    private String sale_price;


    public String getProduct_id() {
        return product_id;
    }

    public void setProduct_id(String product_id) {
        this.product_id = product_id;
    }

    public String getCatalog_no() {
        return catalog_no;
    }

    public void setCatalog_no(String catalog_no) {
        this.catalog_no = catalog_no;
    }

    public String getMrp() {
        return mrp;
    }

    public void setMrp(String mrp) {
        this.mrp = mrp;
    }

    public String getSale_price() {
        return sale_price;
    }

    public void setSale_price(String sale_price) {
        this.sale_price = sale_price;
    }
}


```

to call api use this

```
   public static PriceGroupResponse postToServerGzipGsonPriceGroup(String token, String url, List<CustomNameValuePair> params) throws IOException {
        Log.d("<> URL <>", url);
        PriceGroupResponse response_gson = null;

        URL postURL = new URL(url);
        HttpURLConnection con = (HttpURLConnection) postURL.openConnection();

        con.setRequestProperty("Accept", "application/json");
        con.setRequestProperty("ContentType", "application/json");
        con.setRequestProperty("Authorization", "Bearer " + token);
        con.setRequestProperty("Accept-Encoding", "gzip");
        con.setConnectTimeout(100 * 1000);
        con.setReadTimeout(300 * 1000);
        con.setRequestMethod("POST");
        con.setDoInput(true);
        con.setDoOutput(true);

        OutputStream os = con.getOutputStream();
        BufferedWriter writer = new BufferedWriter(new OutputStreamWriter(os, "UTF-8"));
        writer.write(generatePOSTParams(params));
        writer.flush();
        writer.close();
        os.close();

        con.connect();

        int status = con.getResponseCode();
        switch (status) {
            case 200:
            case 201:

                Reader reader = null;
                if ("gzip".equals(con.getContentEncoding())) {
                    reader = new InputStreamReader(new GZIPInputStream(con.getInputStream()));

                } else {
                    reader = new InputStreamReader(con.getInputStream());
                }

                Gson gson = new Gson();
                response_gson = gson.fromJson(reader, PriceGroupResponse.class);

        }


        return response_gson;
    }


```
other usefull methods and classes

```

    private static String generatePOSTParams(List<CustomNameValuePair> params) throws UnsupportedEncodingException {
        StringBuilder result = new StringBuilder();
        boolean first = true;

        for (CustomNameValuePair pair : params) {
            if (pair != null) {
                if (first)
                    first = false;
                else
                    result.append("&");

                result.append(URLEncoder.encode(pair.getName(), "UTF-8"));
                result.append("=");
                result.append(URLEncoder.encode(pair.getValue(), "UTF-8"));
            }
        }

        Log.d("ERROR", "Server REQUEST : " + result.toString());
        Log.d("ERROR", "Upload size : " + result.toString().getBytes().length + " bytes");

        return result.toString();
    }
    
    
    public class CustomNameValuePair {

    private String name, value;

    public CustomNameValuePair(String name, String value) {
        this.name = name;
        this.value = value;
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public String getValue() {
        return value;
    }

    public void setValue(String value) {
        this.value = value;
    }

    @Override
    public String toString() {
        return name + " : " + value;
    }
}

    
```

