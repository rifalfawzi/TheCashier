#Program Calculator

Aplikasi ini berfungsi untuk menambahkan sebuah item, biasanya di gunakan
untuk menjual sebuah barang/jasa

# Fungsi
- Kalian bisa menambahkan sebuah item
- kaliah bisa memberikan harga
- kalian bisa memencet tombol "Tambahkan"

#Cara Kerja

Diawali dengan "MainWindows" pada class "MainWindows.xaml.cs" kita mendeklarasikan sebuah fungsi calculator

....csharp
public partial class MainWindow : Window
    {
        private Calculator calculator;
        public MainWindow()
        {
            InitializeComponent();
            calculator = new Calculator();
            listBox.ItemsSource = calculator.getListItem();
        }

        private void AddButton_click(object sender, DependencyPropertyChangedEventArgs e)
        {
            string title = itemNameBox.Text;
            int quantity = int.Parse(quantityBox.Text);
            string type = typeBox.Text;
            double price = double.Parse(priceBox.Text);

            Item item = new Item(new Random().Next(), title, quantity, type, price);
            calculator.AddItem(item);
            double total = calculator.getTotal();

            totalLabel.Content = string.Format("Rp {0}", total);

            listBox.Items.Refresh();
....

kemudian Class Item "Item.cs"

...csharp
class Item
    {
        private int id;
        public string title { get; set; }
        public int quantity { get; set; }
        public double price { get; set; }
        public double subtotal { get; set; }
        private string type;

        public Item(int id, string title, int quantity, string type, double price)
        {
            this.id = id;
            this.title = title;
            this.quantity = quantity;
            this.type = type;
            this.price = price;
            this.subtotal = subtotal;

        }
        public string getTitle()
        {
            return title;
        }
        public int getQuantity()
        {
            return quantity;
        }
        public double getPrice()
        {
            return price;
        }
        public double getSubTotal()
        {
            subtotal = price * quantity;
            return subtotal;
        }
        public string getType()
        {
            return type;
        }
....
Kemudian ini adalah logika perhitungannya "Calculator.cs"
...csharp
 class Calculator
    {
        private List<Item> ListItem;
        private double total = 0;

        public Calculator()
        {
            this.ListItem = new List<Item>();
        }
        public void AddItem(Item item)
        {
            this.ListItem.Add(item);
            this.total += item.getSubTotal();
        }
        public double getTotal()
        {
            return total;
        }
        public List<Item> getListItem()
        {
            return ListItem;
        }
...

