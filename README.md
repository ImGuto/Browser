import sys
from PyQt5.QtCore import *
from PyQt5.QtWidgets import*
from PyQt5.QtWebEngineWidgets import*

class MainWindow(QMainWindow):
    def __init__(self):
        super(MainWindow, self). __init__()
        self.browser = QWebEngineView()
        self.browser.setUrl(QUrl ('http://www.google.com'))
        self.setCentralWidget(self.browser)
        self.showMaximized()

        navbar = QToolBar()
        self.addToolBar(navbar)

        back_btn = QAction ('Voltar', self)
        back_btn.triggered.connect(self.browser.back)
        navbar.addAction(back_btn)

        reload_bnt = QAction ('Recarregar', self)
        reload_bnt.triggered.connect(self.browser.reload)
        navbar.addAction(reload_bnt)

        home_bnt = QAction('Home', self)
        home_bnt.triggered.connect(self.navigate_home)
        navbar.addAction(home_bnt)

        self.url_bar = QLineEdit()
        self.url_bar.returnPressed.connect(self.navigate_to_url)
        navbar.addWidget(self.url_bar)

        self.browser.urlChanged.connect(self.update_url)

    def navigate_home(self):
        self.browser.setUrl(QUrl('http://www.google.com'))

    def navigate_to_url(self):
        url = self.url_bar.text()
        self.browser.setUrl(QUrl(url))

    def update_url(self, q):
        self.url_barsetText(q.toString())

app = QApplication(sys.argv)
QApplication.setApplicationName('Guto Browser')
window = MainWindow()
app.exec_()
