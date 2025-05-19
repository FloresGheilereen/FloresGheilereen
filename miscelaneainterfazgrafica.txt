import tkinter as tk
from tkinter import messagebox
from tkinter import ttk

def interfaz_uno():
    area_dinamica_limpia()
    tk.Label(area_dinamica, text="Aquí va un mensaje de bienvenida", font=("Arial", 14)).pack(pady=10)
    tk.Button(area_dinamica, text="Botón 1", command=lambda: messagebox.showinfo("Título", "Mensaje temporal")).pack()

def interfaz_dos():
    area_dinamica_limpia()
    tk.Label(area_dinamica, text="Aquí coloca un letrero o label que identifique al alumno", font=("Arial", 14)).pack(pady=10)

    tk.Label(area_dinamica, text="Campo A:").pack()
    campo_texto_uno = tk.Entry(area_dinamica)
    campo_texto_uno.pack(pady=5)

    tk.Label(area_dinamica, text="Selección A:").pack()
    opcion_elegida = tk.StringVar(value="Opción 1")
    tk.Radiobutton(area_dinamica, text="Opción 1", variable=opcion_elegida, value="Opción 1").pack()
    tk.Radiobutton(area_dinamica, text="Opción 2", variable=opcion_elegida, value="Opción 2").pack()

    tk.Label(area_dinamica, text="Lista desplegable:").pack()
    combo = ttk.Combobox(area_dinamica, values=["Uno", "Dos", "Tres"])
    combo.pack()
    combo.current(0)

    def accion_guardar():
        valor = campo_texto_uno.get()
        messagebox.showinfo("Revisión", f"Texto: {valor}\nSelección: {opcion_elegida.get()}\nLista: {combo.get()}")

    tk.Button(area_dinamica, text="Botón 2", command=accion_guardar).pack(pady=10)

def interfaz_tres():
    area_dinamica_limpia()
    tk.Label(area_dinamica, text="Configuraciones temporales", font=("Arial", 14)).pack(pady=10)

    colores = ["lightblue", "lightgreen", "lightyellow", "lightgray"]
    tk.Label(area_dinamica, text="Cambiar fondo:").pack()

    def cambiar_color(c):
        ventana_principal.config(bg=c)
        menu_lateral.config(bg=c)
        area_dinamica.config(bg=c)

    for c in colores:
        tk.Button(area_dinamica, text=c, bg=c, width=20, command=lambda col=c: cambiar_color(col)).pack(pady=2)

def interfaz_cuatro():
    area_dinamica_limpia()
    tk.Label(area_dinamica, text="Texto de ayuda que el alumno debe mejorar", font=("Arial", 14)).pack(pady=10)
    contenido = (
        "Explica con tus palabras:\n\n"
        "- ¿Qué hace cada botón?\n"
        "- ¿Qué cambias si modificas un texto?\n"
        "- ¿Cómo cambias un color?\n"
        "- ¿Qué debes renombrar?"
    )
    tk.Label(area_dinamica, text=contenido, justify="left").pack(pady=10)

def area_dinamica_limpia():
    for widget in area_dinamica.winfo_children():
        widget.destroy()

ventana_principal = tk.Tk()
ventana_principal.title("Interfaz para prácticas")
ventana_principal.geometry("500x400")
ventana_principal.config(bg="lightblue")

menu_lateral = tk.Frame(ventana_principal, bg="lightblue", width=120)
menu_lateral.pack(side="left", fill="y")

area_dinamica = tk.Frame(ventana_principal, bg="white")
area_dinamica.pack(side="right", expand=True, fill="both")

tk.Button(menu_lateral, text="Pantalla 1", command=interfaz_uno, width=15).pack(pady=10)
tk.Button(menu_lateral, text="Pantalla 2", command=interfaz_dos, width=15).pack(pady=10)
tk.Button(menu_lateral, text="Pantalla 3", command=interfaz_tres, width=15).pack(pady=10)
tk.Button(menu_lateral, text="Pantalla 4", command=interfaz_cuatro, width=15).pack(pady=10)
tk.Button(menu_lateral, text="Salir", command=ventana_principal.destroy, width=15).pack(pady=30)

interfaz_uno()
ventana_principal.mainloop()
