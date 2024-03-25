# EX01 Developing a Simple Webserver
## Date:24.03.2024

## AIM:
To develop a simple webserver to serve html pages.

## DESIGN STEPS:
### Step 1: 
HTML content creation.

### Step 2:
Design of webserver workflow.

### Step 3:
Implementation using Python code.

### Step 4:
Serving the HTML pages.

### Step 5:
Testing the webserver.

## PROGRAM:
```
<!DOCTYPE html>
<html lang="en">
<head>
    <link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/bootstrap-icons@1.11.3/font/bootstrap-icons.min.css">
    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.3/dist/css/bootstrap.min.css" rel="stylesheet" integrity="sha384-QWTKZyjpPEjISv5WaRU9OFeRpok6YctnYmDr5pNlyT2bRjXh0JMhjY6hW+ALEwIH" crossorigin="anonymous">
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>WEB pROJECT</title>
</head>
<style>
    
    body {
        font-family: Arial, sans-serif;
        margin: 0;
        padding: 0;
    }
    #language{
        color: #ffa41b;
    }
    #img {
        background-color:#131921;
        display: flex;
        padding: 5px 10px 1px 10px;
        text-align: left;
    }
    #container {
        max-width: 1200px;
        margin: 0 auto;
        padding: 20px;
    }
    #products {
        display: grid;
        grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
        gap: 20px;
        width: 20%;
    }
    .product {
        border: 1px solid #131921;
        padding: 10px;
        border-radius: 5px;
        background-color:#131921 ;
        color:#ffffff
        
    }
    .product img {
        max-width: 100%;
        height: auto;
        
    
    }
    .about{
        font-size: 12px;
        text-align: center;
        padding-top: 10px;
        
    
    }
    #search-box {
        width: 46%;
        padding: 10px;
        border: 1px solid #ccc;
        border-radius: 5px;
        box-sizing: border-box;
        font-size: 16px;
        height: 40px;
    }
    #search-button{
        padding: 10px 20px;
        background-color: #ffa41b;
        color: #ffffff;
        border: none;
        border-radius: 5px;
        cursor: pointer;
        font-size: 16px;
        width: 3%;
        height: 40px;
    }
    .text{
        font-family: inherit;
        font-size: large;
        padding-top: 2%;
    }
    #text{
        color:gray
    }
    .last{
        font-size: 14px;
    }
    .last1{
        text-decoration: none;
        font-size: small;
        color: #ddd;
    }
</style>
</head>
<body>
<div>
    <div id="img">
        <a href="https://www.amazon.in/ref=nav_logo"><img src="https://pngimg.com/uploads/amazon/amazon_PNG25.png" alt="" width="100px" id='img'></a>
        <a href="https://www.amazon.in/ap/signin?openid.pape.max_auth_age=900&openid.return_to=https%3A%2F%2Fwww.amazon.in%2Fcustomer-preferences%2Fedit%3Fie%3DUTF8%26useRedirectOnSuccess%3D1%26ref_%3Ddex_glow_signin%26path%3D%2Fcustomer-preferences%2Fedit&openid.assoc_handle=inflex&openid.mode=checkid_setup&openid.ns=http%3A%2F%2Fspecs.openid.net%2Fauth%2F2.0" style="color: white; padding: 15px;padding-right:30px; text-decoration:none; color: #ffffff; height:10px" ><i class="bi bi-geo-alt-fill"  ></i>Update Location</a>
        <input type="text" id="search-box" placeholder="Search Amazon.in ..." >
        <button id="search-button"  ><i class="bi bi-search"></i></button>
        <select class="product" >
            <option  value="English">English</option >
            <option value="es">Spain</option>
            <option value="fr">French</option>
            <option value="de">Germany</option>
        </select>
        <a href="https://www.amazon.in/ap/signin?openid.pape.max_auth_age=900&openid.return_to=https%3A%2F%2Fwww.amazon.in%2Fcustomer-preferences%2Fedit%3Fie%3DUTF8%26useRedirectOnSuccess%3D1%26ref_%3Ddex_glow_signin%26path%3D%2Fcustomer-preferences%2Fedit&openid.assoc_handle=inflex&openid.mode=checkid_setup&openid.ns=http%3A%2F%2Fspecs.openid.net%2Fauth%2F2.0" style="color: #ffffff; padding: 15px;padding-right:30px; text-decoration:none; color: #ffffff;font-size:small; " >Hello,sign in!!  </a>
        <a href="https://www.amazon.in/ap/signin?openid.pape.max_auth_age=0&openid.return_to=https%3A%2F%2Fwww.amazon.in%2Fyour-orders%2Forders%3F_encoding%3DUTF8%26ref_%3Dnav_orders_first&openid.identity=http%3A%2F%2Fspecs.openid.net%2Fauth%2F2.0%2Fidentifier_select&openid.assoc_handle=amzn_retail_yourorders_in&openid.mode=checkid_setup&language=en_IN&openid.claimed_id=http%3A%2F%2Fspecs.openid.net%2Fauth%2F2.0%2Fidentifier_select&openid.ns=http%3A%2F%2Fspecs.openid.net%2Fauth%2F2.0 "style="color: #ffffff; padding: 15px;padding-right:20px; text-decoration:none; color: #ffffff;font-size:small; " >Return & Orders</a >
        <a href="https://www.amazon.in/gp/cart/view.html?ref_=nav_cart" style="text-decoration:none; color:#ffffff; padding-top:11px; height:10px ; "><i class="bi bi-cart2"></i>Carts</a>
        <a href="https://www.amazon.in/gp/help/customer/display.html?nodeId=508510&ref_=nav_em_cs_help_0_1_1_38" style="text-decoration: none; padding-left:30px;text-align:center; padding-top:12px; color:#ffffff ">Customer Service</a>
    </div>
    <div class="row row-cols-2 row-cols-md-4 g-12;" style=" display:flex ">
        <div class="col " style="width: 25%; padding:20px; padding-left:30px; height:500px">
          <div class="card h-100" style="height: 300px;">
            <a href="https://www.amazon.in/b/?_encoding=UTF8&node=1380442031&pd_rd_w=oD36U&content-id=amzn1.sym.d0f666fd-1868-4a33-812f-d43daefe4b63&pf_rd_p=d0f666fd-1868-4a33-812f-d43daefe4b63&pf_rd_r=0YD9XPA3M0GKA6Q2H9P3&pd_rd_wg=Ypn1F&pd_rd_r=7fcb3567-edd7-42dc-acc4-27807e1d54a8&ref_=pd_gw_unk"><img src="https://ikiru.in/cdn/shop/products/buy-cushion-cover-leaf-printed-cotton-cushion-cover-for-sofa-by-house-this-on-ikiru-online-store-1_700x700.webp?v=1693561972" height="350px" class="card-img-top" alt="..."></a>
            <h6 class="card-title" style="color: gray;">Cushion covers , bedsheets & more.</h6>
            <p class="text"><b> Revamp your home in style</b></p>
          </div>
        </div>
        <div class="col "  style="width: 25%; padding:20px" >
          <div class="card h-100">
            <a href="https://www.amazon.in/b/?_encoding=UTF8&node=1380485031&pd_rd_w=oD36U&content-id=amzn1.sym.d0f666fd-1868-4a33-812f-d43daefe4b63&pf_rd_p=d0f666fd-1868-4a33-812f-d43daefe4b63&pf_rd_r=0YD9XPA3M0GKA6Q2H9P3&pd_rd_wg=Ypn1F&pd_rd_r=7fcb3567-edd7-42dc-acc4-27807e1d54a8&ref_=pd_gw_unk"><img src="https://specialyou.in/cdn/shop/files/81a3yjFQ6zL._SL1500.jpg?v=1707397652&width=2048" class="card-img-top" alt="..." style="height: 350px;"></a>
              <h6 style="color: gray;" class="card-title">Lights Solution & more</h6>
              <p class="text"><b>Explore the wide range of indoor lighting for your car at Amazon India.</b></p>
             
          </div>
        </div>
        <div class="col " style="width: 25%; padding:20px">
          <div class="card h-100" >
            <a href="https://www.amazon.in/b?node=1968024031"><img src="https://img.freepik.com/premium-photo/modern-boutique-displays-clothing-hangers-defining-stylish-clothes-shopping-experience_896558-6058.jpg" class="card-img-top" alt="..." style="height: 350px;"></a>
            
              <h6 id="text" class="card-title">Clothing</h6>
              <p class="text"><b>Up to 60% off | Styles for men.</b></p>
            
          </div>
        </div>
        <div class="col" style="width: 25%; padding:20px; ">
          <div class="card h-100" >
            <a href="https://www.amazon.in/b/?_encoding=UTF8&node=1380510031&pd_rd_w=oD36U&content-id=amzn1.sym.d0f666fd-1868-4a33-812f-d43daefe4b63&pf_rd_p=d0f666fd-1868-4a33-812f-d43daefe4b63&pf_rd_r=0YD9XPA3M0GKA6Q2H9P3&pd_rd_wg=Ypn1F&pd_rd_r=7fcb3567-edd7-42dc-acc4-27807e1d54a8&ref_=pd_gw_unk" ><img src="https://stownest.com/blog/uploads/images/image_750x_6350f64e8e81e.jpg" class="card-img-top" alt="..." style="height: 300px;"></a>
              <h6 class="card-title" id="text">House Storage</h6>
              <p class="text"><b>Unclutter your entire home with the range of home storage and organisation products that are available at Amazon.in.</b></p>
          </div>
        </div>
        <div class="col" style="width: 25%; padding:20px;height:475px ">
            <div class="card h-100">
              <a href="https://www.amazon.in/s?bbn=84514752031&rh=n%3A84514752031%2Cp_85%3A10440599031&_encoding=UTF8&content-id=amzn1.sym.58c90a12-100b-4a2f-8e15-7c06f1abe2be&pd_rd_r=7fcb3567-edd7-42dc-acc4-27807e1d54a8&pd_rd_w=kx4tW&pd_rd_wg=Ypn1F&pf_rd_p=58c90a12-100b-4a2f-8e15-7c06f1abe2be&pf_rd_r=0YD9XPA3M0GKA6Q2H9P3&ref=pd_gw_unk"><img src="https://aws-obg-image-lb-2.tcl.com/content/dam/brandsite/region/in/blog/pc/detail/blog-march/washing-machine-dimensions/banner.jpg" class="card-img-top" alt="..." style="height: 300px;"></a>
                <h6 class="card-title" id="text">Washing Machines</h6>
                <p class="text"><b>Shop Washing Machine on Amazon.in at best price.</b></p>
            
            </div>
        </div>
       <div class="col " style="width: 25%; padding:20px ; " >
        <div class="card h-100">
          <a href="https://www.amazon.in/ref=fj/b/?_encoding=UTF8&node=5210079031&pd_rd_w=afIcJ&content-id=amzn1.sym.74f25a9d-e850-443b-a26a-da459bed7e95&pf_rd_p=74f25a9d-e850-443b-a26a-da459bed7e95&pf_rd_r=0YD9XPA3M0GKA6Q2H9P3&pd_rd_wg=Ypn1F&pd_rd_r=7fcb3567-edd7-42dc-acc4-27807e1d54a8&ref_=pd_gw_unk"><img src="https://www.krishnajewellers.com/blog/wp-content/uploads/2021/07/RV_10-1100x734.jpg" class="card-img-top" alt="..." style="height: 300px;"></a>
            <h6 id="text" class="card-title">Diamonds and Jewellery</h6>
            <p class="text"><b>Buy trending jewellery designs for women, girls & men at best prices.</b></p>
        
        </div>
       </div>
       <div class="col " style="width: 25%; padding:20px  ;">
        <div class="card h-100">
          <a href="https://www.amazon.in/s?i=fashion&rh=n%3A87295952031%2Cp_36%3A19900-&s=luggage&fs=true&_encoding=UTF8&content-id=amzn1.sym.f34116c1-3bbf-4330-a06d-35e88a4422a0&pd_rd_r=7fcb3567-edd7-42dc-acc4-27807e1d54a8&pd_rd_w=K4lRj&pd_rd_wg=Ypn1F&pf_rd_p=f34116c1-3bbf-4330-a06d-35e88a4422a0&pf_rd_r=0YD9XPA3M0GKA6Q2H9P3&qid=1690908433&rnid=1318502031&ref=pd_gw_unk"><img src="https://www.bhg.com/thmb/CmNRhAddJ0uDEVBD0_T2R0fN3d8=/1866x0/filters:no_upscale():strip_icc()/shelf-purses-wallets-1ozUts30a_8AwLjl-5ORN4-671480b4cf3e4335b2294d9fa0377593.jpg" class="card-img-top" alt="..." style="height: 300px;"></a>
            <h6 id="text" class="card-title">Bags And Wallets</h6>
            <p class="text"><b>Shop for Bags, Wallets, Luggage & other Travel Accessories from Top Brands. Buy now! Best Deals!</b></p>
        
        </div>
       </div>
       <div class="col" style="width: 25%; padding:20px">
        <div class="card h-100">
          <a href="https://www.amazon.in/b/?_encoding=UTF8&node=1983518031&pd_rd_w=K4lRj&content-id=amzn1.sym.f34116c1-3bbf-4330-a06d-35e88a4422a0&pf_rd_p=f34116c1-3bbf-4330-a06d-35e88a4422a0&pf_rd_r=0YD9XPA3M0GKA6Q2H9P3&pd_rd_wg=Ypn1F&pd_rd_r=7fcb3567-edd7-42dc-acc4-27807e1d54a8&ref_=pd_gw_unk"><img src="https://img.buzzfeed.com/store-an-image-prod-us-east-1/qoM28jZUy.png" class="card-img-top" alt="..." style="height: 300px;"></a>
            <h6 id="text" class="card-title">FootWear And Shoes </h6>
            <p class="text"><B>Wide range of Shoes for Men. Choose from loafers, floaters, sports shoes & more. Buy now!</B></p>
        </div>
       </div>
       <div class="col" style="width: 25%; padding:20px;height:450px;">
        <div class="card h-100">
          <a href="https://www.amazon.in/s?bbn=84514739031&rh=n%3A84514739031%2Cp_85%3A10440599031&_encoding=UTF8&content-id=amzn1.sym.58c90a12-100b-4a2f-8e15-7c06f1abe2be&pd_rd_r=7fcb3567-edd7-42dc-acc4-27807e1d54a8&pd_rd_w=kx4tW&pd_rd_wg=Ypn1F&pf_rd_p=58c90a12-100b-4a2f-8e15-7c06f1abe2be&pf_rd_r=0YD9XPA3M0GKA6Q2H9P3&ref=pd_gw_unk"><img src="https://img.etimg.com/thumb/width-1600,height-900,imgsize-47640,resizemode-75,msid-92847221/top-trending-products/kitchen-dining/microwave/best-microwave-oven-under-30000.jpg" class="card-img-top" alt="..." style="height: 300px;"></a>
            <h6 id="text" class="card-title">Microwaves</h6>
            <p class="text"><b>Get up to 55% OFF on Microwaves & Ovens - Grill, Convection & more Compare prices.</b></p>
        </div>
       </div>
       <div class="col" style="width: 25%; padding:20px">
        <div class="card h-100">
          <a href="https://www.amazon.in/s?k=bathroom+hardware+and+accessories&rh=n%3A3704992031%2Cp_n_pct-off-with-tax%3A2665399031&_encoding=UTF8&content-id=amzn1.sym.f7b92a05-ffab-4af4-92d1-a84854a67050&pd_rd_r=7fcb3567-edd7-42dc-acc4-27807e1d54a8&pd_rd_w=Z6Cqa&pd_rd_wg=Ypn1F&pf_rd_p=f7b92a05-ffab-4af4-92d1-a84854a67050&pf_rd_r=0YD9XPA3M0GKA6Q2H9P3&ref=pd_gw_unk"><img src="https://static.independent.co.uk/2024/01/30/17/Bath%20towels-hero.png?width=1200&height=1200&fit=crop" class="card-img-top" alt="..." style="height: 300px;"></a>
            <h6 id="text" class="card-title">Bathroom HardWare And Accessories</h6>
            <p class="text"><b>Choose From a Great Selection Of Cleaning Supplies, Power & Hand Tools & More.</b></p>
          
        </div>
       </div>
       <div class="col" style="width: 25%; padding:20px">
        <div class="card h-100" >
          <a href="https://www.amazon.in/gp/browse.html?node=1389401031&ref_=nav_em_sbc_mobcomp_all_mobiles_0_2_8_2"><img src="https://1.img-dpreview.com/files/p/E~C148x0S885x885T1200x1200~articles/8252062379/samsung-galaxy-fold-3-3.jpeg" class="card-img-top" alt="..." style="height: 300px;"></a>
            <h6 class="card-title" id="text">Smart Phones And Gadgets</h6>
            <p class="text"><b>Grab up to 40% off on Smartphones at Amazon.in. Explore a wide range of the latest smartphones from top brands.</b></p>
        </div>
       </div>
       <div class="col" style="width: 25%; padding:20px">
        <div class="card h-100" >
          <a href="https://www.amazon.in/gp/browse.html?node=976392031&ref_=nav_em_sbc_mobcomp_all_comp_0_2_8_14"><img src="https://i.ytimg.com/vi/N6cFknYffdI/maxresdefault.jpg" class="card-img-top" alt="..." style="height: 300px;"></a>
            <h6 class="card-title" id="text">Laptops and more Accessories</h6>
            <p class="card-text"><b>Discover the best Laptop Computers in Best Sellers. Find the top 100 most popular items in Amazon Electronics Best Sellers.</b></p>
        </div>
       </div>
    </div>   
    <div style="background-color: #004B91;">
        <a href="http://127.0.0.1:5501/webproject.html" style=" text-decoration:none; color:#ffffff ;padding-top:12px" class="about" ><p style="padding-top: 12px;">Back To Top</p></a>
       <div style="background-color: #131921;color:#ffffff; padding-left:25%;display:flex">
        
        <div style="padding-top:50px; padding-right:20px">
          <a href="https://www.aboutamazon.in/?utm_source=gateway&utm_medium=footer" class="last1"><p class="last1">About Us</p></a>
          <a href="https://amazon.jobs/en/" class="last1"><p class="last1">Carrers</p></a>
          <a href="https://press.aboutamazon.in/?utm_source=gateway&utm_medium=footer" style="text-decoration: none;"><p class="last1"> Press Releases</p></a>
          <a href="https://www.amazon.in/ref=nav_logo"><img src="https://pngimg.com/uploads/amazon/amazon_PNG25.png" alt="" width="200px" id='img'></a>  
        </div>

       </div> 
    
        
     
    </div>
</div>


</body>
<script src="https://cdn.jsdelivr.net/npm/bootstrap@5.3.3/dist/js/bootstrap.bundle.min.js" integrity="sha384-YvpcrYf0tY3lHB60NNkmXc5s9fDVZLESaAA55NDzOxhy9GkcIdslK1eN7N6jIeHz" crossorigin="anonymous"></script>
</html>
```

## OUTPUT:

![alt text](<Screenshot 2024-03-25 215317.png>)

![alt text](<Screenshot 2024-03-25 215331.png>)

![alt text](<Screenshot 2024-03-25 215348.png>)


## RESULT:
The program for implementing simple webserver is executed successfully.
