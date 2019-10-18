# GSONANDROID
How to download data using gson and store it in a android app

### json preview 

```
{
    "result": true,
    "priceGroup": [
        {
            "priceG_Id": 13368,
            "price_list_no": "BDGT",
            "priceG_Name": "BUDGET PRICE LIST",
            "items": [
                {
                    "product_id": 4042,
                    "catalog_no": "30WLT120",
                    "mrp": "3850.00",
                    "sale_price": "2845.65"
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

