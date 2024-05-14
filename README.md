import sqlite3

# اتصال بقاعدة البيانات أو إنشاء قاعدة بيانات جديدة إذا لم تكن موجودة
conn = sqlite3.connect('veterinary_clinic.db')

# إنشاء مؤشر للتفاعل مع قاعدة البيانات
cursor = conn.cursor()

# إنشاء جدول لتخزين بيانات الأدوية
cursor.execute('''
    CREATE TABLE IF NOT EXISTS medicines (
        id INTEGER PRIMARY KEY AUTOINCREMENT,
        name TEXT,
        quantity INTEGER,
        price REAL,
        code TEXT
    )
''')

# دالة لإضافة دواء جديد
def add_medicine(name, quantity, price, code):
    cursor.execute('INSERT INTO medicines (name, quantity, price, code) VALUES (?, ?, ?, ?)', (name, quantity, price, code))
    conn.commit()

# دالة لاستعراض جميع الأدوية
def view_medicines():
    cursor.execute('SELECT * FROM medicines')
    medicines = cursor.fetchall()
    for medicine in medicines:
        print(medicine)

# استخدام دالة add_medicine لإضافة دواء جديد
add_medicine('Medicine A', 10, 20.5, 'A123')
add_medicine('Medicine B', 15, 15.75, 'B456')

# استخدام دالة view_medicines لاستعراض جميع الأدوية
view_medicines()

# إغلاق الاتصال بقاعدة البيانات
conn.close()
