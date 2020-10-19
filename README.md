# my_code
Código prueba lectura ficheros xml
# Procesamiento documento rss.xml con método SAX

import xml.sax

# Ahora creamos nuestro manejador de eventos, que será un clase con sus distintos métodos. Usamos la función ContentHandler

class ManejadorEventosCatalogo(xml.sax.ContentHandler):
# Definimos los atributos propios
    def __init__(self):
        self.title = ""
        self.link = ""
        self.description = ""
        self.noticia_iterable = ""        
    def startElement(self,etiqueta,atributos):
        self.noticia_iterable=etiqueta
        
    def endElement(self,etiqueta):
        
        if self.noticia_iterable == 'title':
            print('Title: ',self.title)
        elif self.noticia_iterable == 'link':
            print('Link: ',self.link)    
        elif self.noticia_iterable == 'description':
            print('Description: ',self.description)
            print('***********')
        self.noticia_iterable = ''
        
    def characters(self,contenido):
        if self.noticia_iterable == 'title':
            self.title = contenido
        elif self.noticia_iterable == 'link':
            self.link = contenido
        elif self.noticia_iterable == 'description':
            self.description = contenido
    def startDocument(self):
        print('----------------------------------------')
        print('Comienzo del procesamiento del archivo')
        print('----------------------------------------\n')
        
    def endDocument(self):
        print('----------------------------------------')
        print('Fin del procesamiento del archivo xml')
        print('----------------------------------------')        
if ( __name__ == "__main__"):
    # Creamos un analizador de eventos
    analizador_make_parser = xml.sax.make_parser()
    # Desactivamos los espacios de nombres ya que vamos a trabajar con etiquetas.
    analizador_make_parser.setFeature(xml.sax.handler.feature_namespaces,
                                     False)

    Handler = ManejadorEventosCatalogo()
    analizador_make_parser.setContentHandler(Handler)
   
    analizador_make_parser.parse("rss.xml")   
