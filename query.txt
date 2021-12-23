// 1.Find all the information about each products
db.product.find({}).pretty().toArray();
// 2.Find the product price which are between 400 to 800
db.product.find({ product_price: { $gt: 400, $lt: 800 } }).pretty();
// 3.Find the product price which are not between 400 to 600
db.product.find({ product_price: { $not: { $gt: 400, $lt: 800 } } }).pretty();
// 4.List the four product which are grater than 500 in price
db.product.find({ product_price: { $gt: 500 } }).pretty();
// 5.Find the product name and product material of each products
db.product.find({}, { product_name: 1, product_material: 1 }).pretty();
// 6.Find the product with a row id of 10
db.product.find({ id: "10" }).pretty();
// 7.Find only the product name and product material
db.product.find({}).forEach(function (x) {
  print(
    "product_name: " + x.product_name,
    "product_material:" + x.product_material
  );
});
// 8.Find all products which contain the value of soft in product material
db.product.find({ product_material: { $eq: "Soft" } }).pretty();
// Find 9.products which contain product color indigo  and product price 492.00
db.product.insertOne({
  id: "26",
  product_name: "Licensed Steel Car",
  product_price: 492.0,
  product_material: "Cotton",
  product_color: "indigo",
});
db.product
  .find({ product_color: { $eq: "indigo" }, product_price: { $eq: 492.0 } })
  .pretty();
// 10.Delete the products which product price value are same
// tofind repeated values
db.product.aggregate([
  { $group: { _id: { product_price: "$product_price" }, count: { $sum: 1 } } },
  { $match: { count: 2 } },
]);
// to delete values
db.product.deleteOne({ product_price: { $eq: 36 } });
db.product.deleteOne({ product_price: { $eq: 47 } });
db.product.deleteOne({ product_price: { $eq: 492 } });
