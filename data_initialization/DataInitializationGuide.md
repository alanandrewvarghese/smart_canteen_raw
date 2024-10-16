# Guide: Initialization Of SmartCanteen Database

<!-- Enable Markdown Preview For Better Interface -->
<!-- Shortcut: Ctrl+K Then V-->

## Step 1: Flush previous data if exists
Execute: `python manage.py flush`

## Step 2: Open shell
Execute: `python manage.py shell`

## Step 3: Add item images (One Time Operation)
+ Remove existing item_image(s) from `media/items` 
+ Add updated item_images to `media/items`
+ Url: [item_images]('https://github.com/alanandrewvarghese/smart_canteen_raw/tree/main/item_images')

## Step 4: Execute initialization code
Run the Following code in shell.
```
import random
from django.contrib.auth.models import User
from common.models import Customer, Item, Staff

def create_staff(username, password, name, phone, email):
    user = User.objects.create_user(username=username, password=password)
    staff = Staff.objects.create(user=user, name=name, phone=phone, email=email)
    return staff

def create_customers(customer_data):
    for username, name, email in customer_data:
        user = User.objects.create_user(username=username, password='Pass!123')
        has_khatta = random.choice([True, False])
        customer = Customer.objects.create(user=user, name=name, email=email, has_khatta=has_khatta)
        print(customer)

def add_item(item_name, price, category, food_type, image_name, quantity):
    item = Item(
        item_name=item_name,
        price=price,
        category=category,
        food_type=food_type,
        item_image=f'items/{image_name}',
        quantity=quantity
    )
    item.save()
    print(f"Added {item_name} with quantity {quantity}")

def create_items(item_details):
    quantities = [0] * 10 + [random.randint(1, 20) for _ in range(len(item_details) - 10)]
    random.shuffle(quantities)

    for (item_name, price, category, food_type, image_name), quantity in zip(item_details, quantities):
        add_item(item_name, price, category, food_type, image_name, quantity)

# Staff Creation
create_staff('john', 'John!123', 'John Doe', '9887776666', 'john@gmail.com')

# Customer Creation
customer_data = [
    ('ajithkumar', 'Ajith Kumar', 'ajithkumar@gmail.com'),
    ('amalraj', 'Amal Raj', 'amalraj@gmail.com'),
    ('anilkumar', 'Anil Kumar', 'anilkumar@gmail.com'),
    ('bijumon', 'Biju Mon', 'bijumon@gmail.com'),
    ('chandradas', 'Chandra Das', 'chandradas@gmail.com'),
    ('deepak', 'Deepak Nair', 'deepak@gmail.com'),
    ('gopikrishna', 'Gopi Krishna', 'gopikrishna@gmail.com'),
    ('harikrishnan', 'Hari Krishnan', 'harikrishnan@gmail.com'),
    ('jayakrishnan', 'Jaya Krishnan', 'jayakrishnan@gmail.com'),
    ('kiran', 'Kiran Kumar', 'kiran@gmail.com'),
    ('laljith', 'Laljith Menon', 'laljith@gmail.com'),
    ('manojkumar', 'Manoj Kumar', 'manojkumar@gmail.com'),
    ('narayanan', 'Narayanan Nair', 'narayanan@gmail.com'),
    ('pradeep', 'Pradeep Kumar', 'pradeep@gmail.com'),
    ('ramesh', 'Ramesh Menon', 'ramesh@gmail.com'),
    ('sanjay', 'Sanjay Mohan', 'sanjay@gmail.com'),
    ('sureshkumar', 'Suresh Kumar', 'sureshkumar@gmail.com'),
    ('vijayakumar', 'Vijaya Kumar', 'vijayakumar@gmail.com'),
    ('vimal', 'Vimal Raj', 'vimal@gmail.com'),
    ('yadav', 'Yadav Krishnan', 'yadav@gmail.com')
]
create_customers(customer_data)

# Item Creation
item_details = [
    ('7up', 40.00, 'DR', 'VG', '7up.png'),
    ('Alfaham Mandi', 240.00, 'LN', 'NG', 'alfaham_mandi.png'),
    ('Beef Roast', 130.00, 'CR', 'NG', 'beef_roast.png'),
    ('Black Forest', 60.00, 'DS', 'VG', 'black_forest.png'),
    ('Cakes', 100.00, 'DS', 'VG', 'cakes.png'),
    ('Chapati', 10.00, 'BF', 'VG', 'chapati.png'),
    ('Chicken Biriyani', 150.00, 'LN', 'NG', 'chicken_biriyani.png'),
    ('Chicken Curry', 100.00, 'CR', 'NG', 'chicken_curry.png'),
    ('Chicken Cutlet', 20.00, 'SK', 'NG', 'chicken_cutlet.png'),
    ('Chicken Noodles', 120.00, 'LN', 'NG', 'chicken_noodles.png'),
    ('Chocolate Shake', 80.00, 'DR', 'VG', 'chocolate_shake.png'),
    ('Coffee', 20.00, 'DR', 'VG', 'coffee.png'),
    ('Cupcake', 60.00, 'DS', 'VG', 'cupcake.png'),
    ('Egg Roast', 40.00, 'CR', 'NG', 'egg_roast.png'),
    ('Fried Rice', 120.00, 'LN', 'VG', 'fried_rice.png'),
    ('Gobi Manchurian', 100.00, 'CR', 'VG', 'gobi_manchurian.png'),
    ('Ice Cream', 50.00, 'DS', 'VG', 'ice_cream.png'),
    ('Idli', 8.00, 'BF', 'VG', 'idli.png'),
    ('Kadala Curry', 30.00, 'CR', 'VG', 'kadala_curry.png'),
    ('Masala Dosa', 50.00, 'BF', 'VG', 'masala_dosa.png'),
    ('Meals', 80.00, 'LN', 'VG', 'meals.png'),
    ('Meat Burger', 40.00, 'SK', 'NG', 'meat_burger.png'),
    ('Meat Roll', 20.00, 'SK', 'NG', 'meat_roll.png'),
    ('Porotta', 10.00, 'BF', 'VG', 'porotta.png'),
    ('Puttu', 20.00, 'BF', 'VG', 'puttu.png'),
    ('Samoosa', 10.00, 'SK', 'VG', 'samoosa.png'),
    ('Slice', 40.00, 'DR', 'VG', 'slice.png'),
    ('Sprite', 40.00, 'DR', 'VG', 'sprite.png'),
    ('Uzhunnu Vada', 10.00, 'SK', 'VG', 'uzhunnu_vada.png'),
    ('White Forest', 50.00, 'DS', 'VG', 'white_forest.png'),
]
create_items(item_details)
```
