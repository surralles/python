from PyQt5.QtCore import Qt
from PyQt5.QtWidgets import (QApplication, QWidget, QHBoxLayout, QVBoxLayout, QGroupBox, QRadioButton, QPushButton, QLabel)


app = QApplication([])


window = QWidget()
window.setWindowTitle('Tarjeta de memoria')


'''Interfaz para la aplicación de Tarjeta de memoria'''
btn_OK = QPushButton('Responder') # botón de responder
lb_Question = QLabel('¿En qué año se fundó Moscú?') # texto de pregunta


RadioGroupBox = QGroupBox("Opciones de respuesta") # grupo en la pantalla para botones de radio con respuestas
rbtn_1 = QRadioButton('1147')
rbtn_2 = QRadioButton('1242')
rbtn_3 = QRadioButton('1861')
rbtn_4 = QRadioButton('1943')


layout_ans1 = QHBoxLayout()   
layout_ans2 = QVBoxLayout() # los verticales estarán dentro de los horizontales
layout_ans3 = QVBoxLayout()
layout_ans2.addWidget(rbtn_1) # dos respuestas en la primera columna
layout_ans2.addWidget(rbtn_2)
layout_ans3.addWidget(rbtn_3) # dos respuestas en la segunda columna
layout_ans3.addWidget(rbtn_4)


layout_ans1.addLayout(layout_ans2)
layout_ans1.addLayout(layout_ans3) # las columnas están en la misma línea


RadioGroupBox.setLayout(layout_ans1) # el “panel” con opciones de respuesta está listo 


layout_line1 = QHBoxLayout() # pregunta
layout_line2 = QHBoxLayout() # opciones de respuesta o resultados de prueba
layout_line3 = QHBoxLayout() # botón de “Responder”


layout_line1.addWidget(lb_Question, alignment=(Qt.AlignHCenter | Qt.AlignVCenter))
layout_line2.addWidget(RadioGroupBox)


layout_line3.addStretch(1)
layout_line3.addWidget(btn_OK, stretch=2) # el botón debería ser grande
layout_line3.addStretch(1)


# Ahora vamos a colocar las líneas que hemos creado una debajo de la otra:
layout_card = QVBoxLayout()


layout_card.addLayout(layout_line1, stretch=2)
layout_card.addLayout(layout_line2, stretch=8)
layout_card.addStretch(1)
layout_card.addLayout(layout_line3, stretch=1)
layout_card.addStretch(1)
layout_card.setSpacing(5) # los espacios entre el contenido


window.setLayout(layout_card)
window.show()
app.exec()
