# lol3
# импортируем библиотеку tkinter всю сразу
from tkinter import *
from tkinter import filedialog, messagebox
from PIL import Image, ImageTk

# главное окно приложения
window = Tk()
# заголовок окна
window.title('Авторизация')
# размер окна
window.geometry('1000x1000')
# можно ли изменять размер окна - нет
window.resizable(False, False)

# кортежи и словари, содержащие настройки шрифтов и отступов
font_header = ('Arial', 15)
font_entry = ('Arial', 12)
label_font = ('Arial', 11)
base_padding = {'padx': 10, 'pady': 8}
header_padding = {'padx': 10, 'pady': 12}

remember_var =BooleanVar()

# обработчик нажатия на клавишу 'Войти'
def clicked():

# получаем имя пользователя, пароль, телефон и выбранный вариант
    username = username_entry.get()
    password = password_entry.get()
    phone = phone_entry.get()
    remember_me = remember_var.get()

    # выводим в диалоговое окно введенные пользователем данные
    messagebox.showinfo('Заголовок', '{username},{password}, {phone}, {remember_me}'.format(username="Кирилл", password=123, phone=123456789, remember_me=remember_me))



# заголовок формы: настроены шрифт (font), отцентрирован (justify), добавлены отступы для заголовка
# для всех остальных виджетов настройки делаются также
main_label = Label(window, text='Авторизация', font=font_header, justify=CENTER, **header_padding)
# помещаем виджет в окно по принципу один виджет под другим
main_label.pack()

# метка для поля ввода имени
username_label = Label(window, text='Имя пользователя', font=label_font , **base_padding)
username_label.pack()

# поле ввода имени
username_entry = Entry(window, bg='#fff', fg='#444', font=font_entry)
username_entry.pack()

# метка для поля ввода пароля
password_label = Label(window, text='Пароль', font=label_font , **base_padding)
password_label.pack()

# поле ввода пароля
password_entry = Entry(window, bg='#fff', fg='#444', font=font_entry)
password_entry.pack()

phone_label = Label(window, text='Телефон', font=label_font , **base_padding)
phone_label.pack()

phone_entry = Entry(window, bg='#fff', fg='#444', font=font_entry)
phone_entry.pack()

remember_me_checkbox = Checkbutton(window, text='Запомнить меня', variable=remember_var, font=label_font )
remember_me_checkbox.pack(**base_padding)

selected_option = StringVar(value= 'Выберите вариант')

option_label = Label(window, text='Телефон', font=label_font , **base_padding)
option_label.pack()

options = ('Вариант 1','Вариант 2','Вариант 3')
option_menu = OptionMenu(window, selected_option,*options)
option_menu.pack(**base_padding)

# кнопка отправки формы
send_btn = Button(window, text='Войти', command=clicked)
send_btn.pack(**base_padding)

def smena_fona():
    window.config(bg='black')
    main_label.config(bg='black', fg='white')
    username_label.config(bg='black', fg='white')
    password_label.config(bg='black', fg='white')
    phone_label.config(bg='black', fg='white')
    remember_me_checkbox.config(bg='black', fg='white')
    send_btn.config(bg='gray')

# кнопка для изменения фона
bg_button = Button(window, text='Сменить фон на черный', command=smena_fona)
bg_button.pack(**base_padding)
# функция для увеличения размера шрифта
def increase_font_size():
    global font_header, font_entry, label_font

    # увеличиваем размер шрифта на 2
    font_header = ('Arial', font_header[1] + 2)
    font_entry = ('Arial', font_entry[1] + 2)
    label_font = ('Arial', label_font[1] + 2)

    # обновляем текстовые элементы интерфейса
    main_label.config(font=font_header)
    username_label.config(font=label_font)
    password_label.config(font=label_font)
    phone_label.config(font=label_font)
    remember_me_checkbox.config(font=label_font)
    option_label.config(font=label_font)
    option_menu.config(font=font_entry)
    send_btn.config(font=label_font)

# кнопка для уменьшения размера шрифта
decrease_font_bth = Button(window, text='Увеличить шрифт', command=increase_font_size)
decrease_font_bth.pack(**base_padding)

def decrease_font_size():
    global font_header, font_entry, label_font

    font_header = ('Arial', font_header[1] - 2)
    font_entry = ('Arial', font_entry[1] - 2)
    label_font = ('Arial', label_font[1] - 2)

    # обновляем текстовые элементы интерфейса
    main_label.config(font=font_header)
    username_label.config(font=label_font)
    password_label.config(font=label_font)
    phone_label.config(font=label_font)
    remember_me_checkbox.config(font=label_font)
    option_label.config(font=label_font)
    option_menu.config(font=font_entry)
    send_btn.config(font=label_font)

# кнопка для увеличения размера шрифта
decrease_font_bth = Button(window, text='Уменьшить шрифт', command=decrease_font_size)
decrease_font_bth.pack(**base_padding)

def load_image():
    file_path = filedialog.askopenfilename(title="Выберите Изображение",
                                           filetypes=[("Image Files", "*.png;.jpg;*.jpeg;*.gif")])

    if file_path:
        img = Image.open(file_path)
        img.thumbnail((150, 150))
        img_tk = ImageTk.PhotoImage(img)

        image_label.config(image=img_tk)
        image_label.image = img_tk

load_image_bth = Button(window, text='Загрузить изображение', command=load_image)
load_image_bth.pack(**base_padding)

image_label = Label(window)
image_label.pack(pady=(10, 0))

def load_pdf():
    file_path = filedialog.askopenfilename(title="Выберите PDF файл", filetypes=[("PDF Files", "*.pdf")])

    if file_path:
        pdf_entry.delete(0, END)
        pdf_entry.insert(0,file_path)

pdf_label = Label(window, text='Загрузить PDF файл', font=label_font , **base_padding)
pdf_label.pack()

pdf_entry = Entry(window, bg='#fff', fg='#444', font=font_entry)
pdf_entry.pack()

load_pdf_bth = Button(window, text='Выбрать PDF файл', command = load_pdf, font=label_font)
load_pdf_bth.pack(**base_padding)

def open_new_window():
    new_window = Toplevel(window)
    new_window.title("Главное окно")
    new_window.geometry("300x150")

    label = Label(new_window, text="Добро пожаловать!", font=font_header)
    label.pack(pady=20)

    close_bth = Button(new_window, text="Закрыть",command=new_window.destroy)
    close_bth.pack(pady=10)

def clicked():

    username = username_entry.get()
    password = password_entry.get()

    if username and password :
        open_new_window()

# запускаем главный цикл окна
window.mainloop()
