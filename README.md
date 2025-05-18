class Product:
    def __init__(self, name, price, quantity):
        self._name = name
        self._price = price
        self._quantity = quantity
    def get_name(self):
        return self._name
    def get_price(self):
        return self._price
    def get_quantity(self):
        return self._quantity
    def set_price(self, price):
        self._price = price
    def set_quantity(self, quantity):
        self._quantity = quantity
    def __repr__(self):
        return f"Product(name='{self._name}', price={self._price}, quantity={self._quantity})"
product1 = Product("Laptop", 1000, 10)
product2 = Product("Mouse", 20, 50)

print(product1)
print(product2)

class Warehouse(Product):
    def __init__(self):
        super().__init__("", 0, 0)  # Ініціалізація базового класу з порожніми значеннями
        self._products = []
    def add_product(self, product):
        self._products.append(product)
    def find_products_by_name(self, name):
        return [product for product in self._products if product.get_name() == name]
    def find_products_by_price_range(self, min_price, max_price):
        return [product for product in self._products if min_price <= product.get_price() <= max_price]
    def get_products(self):
        return self._products
    def remove_product(self, product):
        if product in self._products:
            self._products.remove(product)
    @staticmethod
    def total_quantity(products):
        return sum(product.get_quantity() for product in products)
    def _total_value(self, products):
        return sum(product.get_price() * product.get_quantity() for product in products)

warehouse = Warehouse()

product1 = Product("Laptop", 1000, 10)
product2 = Product("Mouse", 20, 50)

warehouse.add_product(product1)
warehouse.add_product(product2)

print(warehouse.find_products_by_name("Laptop"))
print(warehouse.find_products_by_price_range(10, 100))
print(warehouse.get_products())

warehouse.remove_product(product1)
print(warehouse.get_products())

print(Warehouse.total_quantity(warehouse.get_products()))
print(warehouse._total_value(warehouse.get_products()))
