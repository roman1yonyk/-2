# import tkinter as tk
# from tkinter import messagebox
# from kivy.app import App
# from kivy.uix.boxlayout import BoxLayout
# from kivy.properties import ObjectProperty


# class Product:
#     def __init__(self, name, price):
#         self.name = name
#         self.price = price

# class ShoppingCart:
#     def __init__(self):
#         self.items = []

#     def add_item(self, product):
#         self.items.append(product)

#     def calculate_total(self):
#         total = sum([item.price for item in self.items])
#         return total

# class App:
#     def __init__(self, master):
#         self.master = master
#         self.master.title("Інтернет-магазин")

#         self.products = [
#             Product("Laptop", 1000,),
#             Product("Phone", 500,),
#             Product("Планшет", 500),
#             Product("Годинник", 200),
#             Product("Камера", 700)
#         ]

#         self.shopping_cart = ShoppingCart()

#         self.create_widgets()

#     def create_widgets(self):
#         self.product_listbox = tk.Listbox(self.master, width=40, height=10)
#         self.product_listbox.grid(row=0, column=0, padx=10, pady=10)

#         for product in self.products:
#             self.product_listbox.insert(tk.END, f"{product.name} - ${product.price}")

#         self.add_to_cart_button = tk.Button(self.master, text="Додати у кошик", command=self.add_to_cart)
#         self.add_to_cart_button.grid(row=1, column=0, padx=10, pady=5)

#         self.total_label = tk.Label(self.master, text="Загальна вартість: $0")
#         self.total_label.grid(row=2, column=0, padx=10, pady=5)

#     def add_to_cart(self):
#         selected_index = self.product_listbox.curselection()
#         if selected_index:
#             selected_product = self.products[selected_index[0]]
#             self.shopping_cart.add_item(selected_product)
#             total_amount = self.shopping_cart.calculate_total()
#             self.total_label.config(text=f"Загальна вартість: ${total_amount}")
#             messagebox.showinfo("Повідомлення", f"{selected_product.name} додано у кошик.")
#         else:
#             messagebox.showwarning("Попередження", "Виберіть товар для додавання у кошик.")

# def main():
#     root = tk.Tk()
#     app = App(root)
#     root.mainloop()

# if __name__ == "__main__":
#     main()


# from kivy.app import App
# from kivy.uix.boxlayout import BoxLayout
# from kivy.uix.label import Label
# from kivy.uix.button import Button
# from kivy.uix.popup import Popup
# from kivy.uix.spinner import Spinner
# from kivy.uix.recycleview import RecycleView

# class Product:
#     def __init__(self, name, price):
#         self.name = name
#         self.price = price

# class ShoppingCart:
#     def __init__(self):
#         self.items = []

#     def add_item(self, product):
#         self.items.append(product)

#     def remove_item(self, product_name):
#         self.items = [item for item in self.items if item.name != product_name]

#     def calculate_total(self):
#         total = sum([item.price for item in self.items])
#         return total

# class ShoppingCartApp(App):
#     def build(self):
#         self.products = [
#             Product("Laptop", 1000),
#             Product("Phone", 500),
#             Product("Планшет", 500),
#             Product("Годинник", 200),
#             Product("Камера", 700)
#         ]

#         self.shopping_cart = ShoppingCart()

#         layout = BoxLayout(orientation='vertical')

#         self.product_spinner = Spinner(text='Виберіть товар')
#         for product in self.products:
#             self.product_spinner.values.append(f"{product.name} - ${product.price}")

#         add_to_cart_button = Button(text='Додати у кошик')
#         add_to_cart_button.bind(on_press=self.add_to_cart)

#         self.total_label = Label(text='Загальна вартість: $0')

#         layout.add_widget(self.product_spinner)
#         layout.add_widget(add_to_cart_button)
#         layout.add_widget(self.total_label)

#         self.cart_button = Button(text='Кошик')
#         self.cart_button.bind(on_press=self.show_shopping_cart)
#         layout.add_widget(self.cart_button)

#         return layout

#     def add_to_cart(self, instance):
#         selected_product = self.product_spinner.text.split(' - ')[0]
#         price = int(self.product_spinner.text.split(' - ')[1].strip('$'))

#         self.shopping_cart.add_item(Product(selected_product, price))
#         total_amount = self.shopping_cart.calculate_total()
#         self.total_label.text = f"Загальна вартість: ${total_amount}"

#         popup = Popup(title='Повідомлення', content=Label(text=f"{selected_product} додано у кошик."), size_hint=(None, None), size=(400, 200))
#         popup.open()

#     def show_shopping_cart(self, instance):
#         cart_layout = BoxLayout(orientation='vertical')
#         cart_popup = Popup(title='Кошик', content=cart_layout, size_hint=(None, None), size=(400, 400))

#         cart_items = RecycleView()
#         cart_data = [{'text': f"{item.name} - ${item.price}"} for item in self.shopping_cart.items]
#         cart_items.data = cart_data

#         cart_layout.add_widget(cart_items)

#         def remove_item_from_cart(button):
#             selected_item = button.text.split(' ')[1]
#             self.shopping_cart.remove_item(selected_item)
#             cart_items.data = [{'text': f"{item.name} - ${item.price}"} for item in self.shopping_cart.items]

#         for item in self.shopping_cart.items:
#             remove_button = Button(text=f"Видалити {item.name}")
#             remove_button.bind(on_press=remove_item_from_cart)
#             cart_layout.add_widget(remove_button)

#         cart_popup.open()

# if __name__ == '__main__':
#     ShoppingCartApp().run()


from kivy.app import App
from kivy.uix.boxlayout import BoxLayout
from kivy.uix.label import Label
from kivy.uix.button import Button
from kivy.uix.popup import Popup
from kivy.uix.spinner import Spinner
from kivy.properties import ObjectProperty

class Product:
    def __init__(self, name, price):
        self.name = name
        self.price = price

class ShoppingCart:
    def __init__(self):
        self.items = []

    def add_item(self, product):
        self.items.append(product)

    def calculate_total(self):
        total = sum([item.price for item in self.items])
        return total

class ShoppingCartApp(App):
    def build(self):
        self.products = [
            Product("Laptop", 1000),
            Product("Phone", 500),
            Product("Планшет", 500),
            Product("Годинник", 200),
            Product("Камера", 700)
        ]

        self.shopping_cart = ShoppingCart()

        layout = BoxLayout(orientation='vertical')

        self.product_spinner = Spinner(text='Виберіть товар')
        for product in self.products:
            self.product_spinner.values.append(f"{product.name} - ${product.price}")

        add_to_cart_button = Button(text='Додати у кошик')
        add_to_cart_button.bind(on_press=self.add_to_cart)

        self.total_label = Label(text='Загальна вартість: $0')

        layout.add_widget(self.product_spinner)
        layout.add_widget(add_to_cart_button)
        layout.add_widget(self.total_label)

        return layout

    def add_to_cart(self, instance):
        selected_product = self.product_spinner.text.split(' - ')[0]
        price = int(self.product_spinner.text.split(' - ')[1].strip('$'))

        self.shopping_cart.add_item(Product(selected_product, price))
        total_amount = self.shopping_cart.calculate_total()
        self.total_label.text = f"Загальна вартість: ${total_amount}"

        popup = Popup(title='Повідомлення', content=Label(text=f"{selected_product} додано у кошик."), size_hint=(None, None), size=(400, 200))
        popup.open()

if __name__ == '__main__':
    ShoppingCartApp().run()
