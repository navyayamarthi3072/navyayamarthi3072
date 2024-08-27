from flask import Flask, request, jsonify
from flask_sqlalchemy import SQLAlchemy

app = Flask(__name__)
app.config["SQLALCHEMY_DATABASE_URI"] = "sqlite:///marketplace.db"
db = SQLAlchemy(app)

class Product(db.Model):
    id = db.Column(db.Integer, primary_key=True)
    name = db.Column(db.String(100), nullable=False)
    description = db.Column(db.String(200), nullable=False)
    price = db.Column(db.Float, nullable=False)

class Order(db.Model):
    id = db.Column(db.Integer, primary_key=True)
    product_id = db.Column(db.Integer, db.ForeignKey("(link unavailable)"))
    quantity = db.Column(db.Integer, nullable=False)

@app.route("/products", methods=["GET"])
def get_products():
    products = Product.query.all()
    return jsonify([{"id": (link unavailable), "name": p.name, "description": p.description, "price": p.price} for p in products])

@app.route("/products", methods=["POST"])
def create_product():
    data = request.get_json()
    product = Product(name=data["name"], description=data["description"], price=data["price"])
    db.session.add(product)
    db.session.commit()
    return jsonify({"message": "Product created successfully"})

@app.route("/orders", methods=["POST"])
def create_order():
    data = request.get_json()
    order = Order(product_id=data["product_id"], quantity=data["quantity"])
    db.session.add(order)
    db.session.commit()
    return jsonify({"message": "Order created successfully"})

if __name__ == "__main__":
    app.run(debug=True)
