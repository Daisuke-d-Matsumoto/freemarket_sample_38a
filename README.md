# README

## social_profilesテーブル

|column|Type|Options|
|------|----|-------|
|provider|string|null: false|
|uid|string|null: false, unique: true|
|token|string||
|nickname|string||
|email|varchar||

### Association
- belongs_to :user

## usersテーブル

|column|Type|Options|
|------|----|-------|
|nickname|string|null: false, unique: true, index: true|
|image|text||
|text|text||

### Association
- belongs_to :social_profile
- belongs_to :user_detail
- belongs_to :point
- belongs_to :credit_card
- belongs_to :deposit
- belongs_to :rate
- belongs_to :address
- belongs_to :birthday
- has_many :products
- has_many :users_news
- has_many :notices
- has_many :todos
- has_many :news
- has_many :transaction_comments
- has_many :product_page_comments
- has_many :likes
- has_many :orders

## noticesテーブル

|column|Type|Options|
|------|----|-------|
|from_user_id|integer|null: false, foreign_key: true|
|to_user_id|integer|null: false, foreign_key: true|
|text|text|null: false|

### Association
- belongs_to :user

## todosテーブル

|column|Type|Options|
|------|----|-------|
|user_id|integer|null: false, foreign_key: true|
|text|text|null: false|

### Association
- belongs_to :user

## news_usersテーブル

|column|Type|Options|
|------|----|-------|
|user_id|integer|null: false, foreign_key: true|
|news_id|integer|null: false, foreign_key: true|

### Association
- belongs_to :user
- belongs_to :news

## newsテーブル

|column|Type|Options|
|------|----|-------|
|title|text|null: false|
|text|text|null: false|
|personal|integer||

### Association
- has_many :users, through: news_users
- has_many :news_users
- accepts_nested_attributes_for :news_users

## ratesテーブル

|column|Type|Options|
|------|----|-------|
|user_id|integer|null: false, foreign_key: true|
|user_detail_id|integer|null: false, foreign_key: true|
|rating|integer|null: false|

### Association
- belongs_to :user
- belongs_to :user_detail

## user_detailsテーブル

|column|Type|Options|
|------|----|-------|
|user_id|integer|null: false, foreign_key: true|
|first_name_kanji|string|null: false|
|last_name_kanji|string|null: false|
|first_name_kana|string|null: false|
|last_name_kana|string|null: false|
|payment|integer||

### Association
- belongs_to :user

## depositsテーブル

|column|Type|Options|
|------|----|-------|
|user_id|integer|null: false, foreign_key: true|
|proceeds|integer||

### Association
- belongs_to :user
- belongs_to :banks

## banksテーブル

|column|Type|Options|
|------|----|-------|
|deposit_id|integer|null: false, foreign_key: true|
|bank_name|string|null: false|
|type|string|null: false|
|branch_code|string|null: false|
|account_number|string|null: false|
|first_name_kana|string|null: false|
|last_name_kana|string|null: false|

### Association
- belongs_to :deposit

## credit_cardsテーブル

|column|Type|Options|
|------|----|-------|
|user_id|integer|null: false, foreign_key: true|
|main_number|string|null: false|
|month|integer|null: false|
|year|integer|null: false|
|security_code|integer|null: false|

### Association
- belongs_to :user

## pointsテーブル

|column|Type|Options|
|------|----|-------|
|user_id|integer|null: false, foreign_key: true|
|point_365|integer||
|point_180|integer||
|effective_term|string|null: false|

### Association
- belongs_to :user

## addressesテーブル

|column|Type|Options|
|------|----|-------|
|user_id|integer|null: false, foreign_key: true|
|postal_code|string|null: false|
|prefecture|text|null: false|
|city|text|null: false|
|street_address|text|null: false|
|building|text||
|phone|string||

### Association
- belongs_to :user

## birthdaysテーブル

|column|Type|Options|
|------|----|-------|
|user_id|integer|null: false, foreign_key: true|
|birth_year|integer||
|birth_month|integer||
|birth_year|integer||

### Association
- belongs_to :user

## productsテーブル

|column|Type|Options|
|------|----|-------|
|user_id|integer|null: false, unique: true, index: true|
|name|string|null: false|
|price|integer|null: false|
|satatus|string|null: false|

### Association
- belongs_to :product_detail
- belongs_to :order
- belongs_to :user
- belongs_to :delivery
- belongs_to :image
- belongs_to :product_detail_brand
- belongs_to :product_detail_category
- has_many :transaction_comments
- has_many :product_page_comments
- has_many :likes

## product_detailsテーブル

|column|Type|Options|
|------|----|-------|
|product_id|integer|null: false, foreign_key: true|
|state_of_goods|text|null: false|
|freight|integer|null: false|
|description|text|null: false|
|size|string||

### Association
- belongs_to :product

## imagesテーブル

|column|Type|Options|
|------|----|-------|
|product_id|integer|null: false, foreign_key: true|
|first_image|text|null: false|
|second_image|text||
|third_image|text||
|forth_image|text||

### Association
- belongs_to :product

## deliveriesテーブル

|column|Type|Options|
|------|----|-------|
|product_id|integer|null: false, foreign_key: true|
|ship_method|string|null: false|
|ship_form_location|string|null: false|
|ship_day|string|null: false|

### Association
- belongs_to :product

## products_brandsテーブル

|column|Type|Options|
|------|----|-------|
|product_detail_id|integer|null: false, foreign_key: true|
|brand_id|integer|null: false, foreign_key: true|

### Association
- belongs_to :product
- belongs_to :brand

## brandsテーブル

|column|Type|Options|
|------|----|-------|
|name|string|null: false, index: true|

### Association
- has_many :products_brands

## products_categoriesテーブル

|column|Type|Options|
|------|----|-------|
|product_id|integer|null: false, foreign_key: true|
|category_id|integer|null: false, foreign_key: true|

### Association
- belongs_to :product
- belongs_to :category

## categoriesテーブル

|column|Type|Options|
|------|----|-------|
|name|string|null: false, index: true|

### Association
- has_many :products_categories

## transaction_commentsテーブル

|column|Type|Options|
|------|----|-------|
|product_id|integer|null: false, foreign_key: true|
|user_id|integer|null: false, foreign_key: true|
|text|text|null: false|

### Association
- belongs_to :product
- belongs_to :user

## product_page_commentsテーブル

|column|Type|Options|
|------|----|-------|
|product_id|integer|null: false, foreign_key: true|
|user_id|integer|null: false, foreign_key: true|
|text|text|null: false|

### Association
- belongs_to :product
- belongs_to :user

## likesテーブル

|column|Type|Options|
|------|----|-------|
|product_id|integer|null: false, foreign_key: true|
|user_id|integer|null: false, foreign_key: true|

### Association
- belongs_to :product
- belongs_to :user

## ordersテーブル

|column|Type|Options|
|------|----|-------|
|product_id|integer|null: false, foreign_key: true|
|user_id|integer|null: false, foreign_key: true|

### Association
- belongs_to :product
- belongs_to :user

This README would normally document whatever steps are necessary to get the
application up and running.

Things you may want to cover:

* Ruby version

* System dependencies

* Configuration

* Database creation

* Database initialization

* How to run the test suite

* Services (job queues, cache servers, search engines, etc.)

* Deployment instructions

* ...
