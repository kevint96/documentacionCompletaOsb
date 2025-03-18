import streamlit as st
import os
import shutil
from zipfile import ZipFile
import zipfile
import tempfile
import subprocess
from io import BytesIO
from docx import Document
from docx.shared import Pt
from docx.shared import RGBColor
from docx.enum.text import WD_PARAGRAPH_ALIGNMENT
from docx.oxml import OxmlElement
import inspect
import os
import xml.etree.ElementTree as ET
import gspread
import time  # Importar el módulo time
import logging
import re
import inspect
import ast
from datetime import datetime
import difflib
import glob
import base64
import sys

def print_with_line_number(msg):
    caller_frame = inspect.currentframe().f_back
    line_number = caller_frame.f_lineno
    print(f"Linea {line_number}: {msg}")
    print("")
    
def apply_format(run,fuente,size,negrita,color):
    run.font.name = fuente  # Cambiar el nombre de la fuente
    run.font.size = Pt(size)  # Cambiar el tamaño de la fuente
    run.font.bold = negrita  # Aplicar negrita
    run.font.color.rgb = RGBColor(0, 0, color)  # Cambiar el color del texto a rojo

def replace_text_in_paragraph(paragraph, replacements):
    full_text = paragraph.text
    contador = 1
    ##st.success(f"Texto en linea: {full_text}")
    for key, value in replacements.items():
        if key in full_text:
            ##st.success(f"full_text: {full_text}")
            ##st.success(f"p paragraphs: {paragraph.text}")
            ##st.success(f"clave coincide: {key}")
            full_text = full_text.replace(key, str(value))  # Actualiza full_text
            
            if key in '{nombre_servicio_inicial}':
                paragraph.clear()  # Limpiar el párrafo
                paragraph.add_run(full_text)  # Agregar el texto actualizado al párrafo
                apply_format(paragraph.runs[0],'Arial',18,True,0)  # Aplicar formato al texto del párrafo
                paragraph.alignment = WD_PARAGRAPH_ALIGNMENT.RIGHT
                
            if key in '{nombre_operacion_inicial}':
                paragraph.clear()  # Limpiar el párrafo
                paragraph.add_run(full_text)  # Agregar el texto actualizado al párrafo
                apply_format(paragraph.runs[0],'Arial',10,True,0)  # Aplicar formato al texto del párrafo
                paragraph.alignment = WD_PARAGRAPH_ALIGNMENT.RIGHT
                
            if key in '{nombre_servicio_secundario}':
                paragraph.clear()  # Limpiar el párrafo
                paragraph.add_run(full_text)  # Agregar el texto actualizado al párrafo
                apply_format(paragraph.runs[0],'Arial',10,True,0)    # Aplicar formato al texto del párrafo
                paragraph.alignment = WD_PARAGRAPH_ALIGNMENT.RIGHT
            
            if key in '{nombre_operacion}':
                paragraph.clear()  # Limpiar el párrafo
                paragraph.add_run(full_text)  # Agregar el texto actualizado al párrafo
                apply_format(paragraph.runs[0],'Times New Roman',10,False,0)    # Aplicar formato al texto del párrafo
                paragraph.alignment = WD_PARAGRAPH_ALIGNMENT.LEFT
            
            if key in '{unique_operations}':
                paragraph.clear()  # Limpiar el párrafo
                paragraph.add_run(full_text)  # Agregar el texto actualizado al párrafo
                apply_format(paragraph.runs[0],'Times New Roman',10,False,0)    # Aplicar formato al texto del párrafo
                paragraph.alignment = WD_PARAGRAPH_ALIGNMENT.LEFT
            
            if key in '{nombre_servicio}':
                paragraph.clear()  # Limpiar el párrafo
                paragraph.add_run(full_text)  # Agregar el texto actualizado al párrafo
                apply_format(paragraph.runs[0],'Times New Roman',10,False,0)    # Aplicar formato al texto del párrafo
                paragraph.alignment = WD_PARAGRAPH_ALIGNMENT.LEFT
            
            if key in '{nombre_servicio_contrato}':
                paragraph.clear()  # Limpiar el párrafo
                paragraph.add_run(full_text)  # Agregar el texto actualizado al párrafo
                apply_format(paragraph.runs[0],'Times New Roman',10,False,0)  # Aplicar formato al texto del párrafo
            
            if key in '{nombre_servicio_wsdl}':
                paragraph.clear()  # Limpiar el párrafo
                paragraph.add_run(full_text)  # Agregar el texto actualizado al párrafo
                apply_format(paragraph.runs[0],'Times New Roman',10,False,0)  # Aplicar formato al texto del párrafo
            
            if key in '{nombre_servicio_contrato2}':
                paragraph.clear()  # Limpiar el párrafo
                paragraph.add_run(full_text)  # Agregar el texto actualizado al párrafo
                apply_format(paragraph.runs[0],'Arial',10,False,0)  # Aplicar formato al texto del párrafo
                
            if key in '{nombre_servicio_tabla}':
                paragraph.clear()  # Limpiar el párrafo
                paragraph.add_run(full_text)  # Agregar el texto actualizado al párrafo
                apply_format(paragraph.runs[0],'Arial MT',11,False,0)  # Aplicar formato al texto del párrafo
            
            if key in '{fecha}':
                paragraph.clear()  # Limpiar el párrafo
                paragraph.add_run(full_text)  # Agregar el texto actualizado al párrafo
                apply_format(paragraph.runs[0],'Arial MT',10,False,0)  # Aplicar formato al texto del párrafo
            
            if key in '{autor_inicial}':
                paragraph.clear()  # Limpiar el párrafo
                paragraph.add_run(full_text)  # Agregar el texto actualizado al párrafo
                apply_format(paragraph.runs[0],'Arial MT',10,True,0)  # Aplicar formato al texto del párrafo
            
            if key in '{autor}':
                paragraph.clear()  # Limpiar el párrafo
                paragraph.add_run(full_text)  # Agregar el texto actualizado al párrafo
                apply_format(paragraph.runs[0],'Arial',10,False,0)  # Aplicar formato al texto del párrafo
            
            if key in '{autor2}':
                paragraph.clear()  # Limpiar el párrafo
                paragraph.add_run(full_text)  # Agregar el texto actualizado al párrafo
                apply_format(paragraph.runs[0],'Arial MT',10,False,0)  # Aplicar formato al texto del párrafo
            
            if key in '{url}':
                paragraph.clear()  # Limpiar el párrafo
                paragraph.add_run(full_text)  # Agregar el texto actualizado al párrafo
                apply_format(paragraph.runs[0],'Arial MT',10,False,255)  # Aplicar formato al texto del párrafo
                
            if key in '{operacion_legado}':
                paragraph.clear()  # Limpiar el párrafo
                paragraph.add_run(full_text)  # Agregar el texto actualizado al párrafo
                apply_format(paragraph.runs[0],'Arial MT',10,False,255)  # Aplicar formato al texto del párrafo
                
            
            if key in '{proyecto_abc}':
                paragraph.clear()  # Limpiar el párrafo
                paragraph.add_run(full_text)  # Agregar el texto actualizado al párrafo
                apply_format(paragraph.runs[0],'Arial MT',10,False,0)  # Aplicar formato al texto del párrafo

def print_element_content(element, element_name):
    #st.success(f"Contenido del {element_name}:")
    for paragraph in element.paragraphs:
        st.success(paragraph.text)
    for table in element.tables:
        for row in table.rows:
            for cell in row.cells:
                for paragraph in cell.paragraphs:
                    st.success(paragraph.text)

def replace_text_in_element(element, replacements):
    for paragraph in element.paragraphs:
        replace_text_in_paragraph(paragraph, replacements)
    for table in element.tables:
        for row in table.rows:
            for cell in row.cells:
                for paragraph in cell.paragraphs:
                    replace_text_in_paragraph(paragraph, replacements)

def replace_text_in_doc(doc, replacements):
    for p in doc.paragraphs:
        replace_text_in_paragraph(p, replacements)

    for table in doc.tables:
        for row in table.rows:
            for cell in row.cells:
                for paragraph in cell.paragraphs:
                    replace_text_in_paragraph(paragraph, replacements)

    for section in doc.sections:
        #st.success(f"Encabezado de la sección: {section.header}")
        print_element_content(section.header, "Encabezado de la sección")
        replace_text_in_element(section.header, replacements)
        #st.success(f"Pie de página de la sección: {section.footer}")
        print_element_content(section.footer, "Pie de página de la sección")
        replace_text_in_element(section.footer, replacements)
        # Agregamos este bloque específico para procesar las tablas dentro del encabezado de la sección 2
        if "Encabezado-Sección 2-" in [paragraph.text for paragraph in section.header.paragraphs]:
            for table in section.header.tables:
                for row in table.rows:
                    for cell in row.cells:
                        for paragraph in cell.paragraphs:
                            st.success(paragraph.text)
            for table in section.header.tables:
                for row in table.rows:
                    for cell in row.cells:
                        for paragraph in cell.paragraphs:
                            replace_text_in_paragraph(paragraph, replacements)
    
    doc = reemplazar_texto_en_doc(doc, replacements)
    
    return doc

   
def service_refs_ruta_pipeline(pipeline_path, project_path):
    
    elemento = ""
    # Servicios a excluir
    servicios_a_excluir = [
        'ComponentesComunes/Proxies/PS_ManejadorGenericoErroresV1.0',
        'UtilitariosEBS/Proxies/AuditoriaSOA/RegistrarAuditoriaSOADATV1.0'
    ]
    
    while True:
        
        #st.success(f"pipeline_path: {pipeline_path}")
        
        # Leer el archivo .pipeline
        with open(pipeline_path, 'r') as file:
            pipeline_content = file.readlines()

        # Buscar todas las líneas que contienen ':service ref="'
        matching_lines = [line for line in pipeline_content if ':service ref="' in line]

        # Extraer la información deseada de las líneas coincidentes
        servicios = set()  # Usamos un conjunto para evitar elementos duplicados
        for line in matching_lines:
            service_start_index = line.find(':service ref="') + len(':service ref="')
            service_end_index = line.find('"', service_start_index)
            service_ref = line[service_start_index:service_end_index]
            # Verificar si el servicio no está en la lista de servicios a excluir
            if service_ref not in servicios_a_excluir:
                servicios.add(service_ref)

        # Imprimir los servicios encontrados
        st.success("Servicios encontrados:")
        for service in servicios:
            st.success(service)
            
             # Si el elemento contiene '/BusinessServices/', salir del bucle
            if '/BusinessServices/' in service:
                #st.success(f"BusinessServices: {service}")
                business_path = os.path.join(project_path, service + '.bix')
                
                with open(business_path, 'r') as business_file:
                    business_content = business_file.readlines()
                    
                    matching_lines = [line for line in business_content if 'operation-name>' in line]
                    
                    # Extraer los elementos ref de las líneas coincidentes
                    elementos_ref = set()  # Usamos un conjunto para evitar elementos duplicados
                    for line in matching_lines:
                        invoke_start_index = line.find('operation-name>') + len('operation-name>')
                        invoke_end_index = line.find('<', invoke_start_index)
                        invoke_ref = line[invoke_start_index:invoke_end_index]
                        elementos_ref.add(invoke_ref)

                    # Imprimir los elementos ref encontrados
                    st.success("Elementos ref encontrados en {}: ".format(service))
                    for elemento in elementos_ref:
                        st.success(elemento)
                return elemento

            # Construir la ruta del archivo proxy
            proxy_path = os.path.join(project_path, service + '.proxy')

            # Verificar si el archivo proxy existe
            if os.path.exists(proxy_path):
                # Leer el archivo proxy
                with open(proxy_path, 'r') as proxy_file:
                    proxy_content = proxy_file.readlines()

                # Buscar todas las líneas que contienen ':invoke ref="'
                matching_lines = [line for line in proxy_content if ':invoke ref="' in line]

                # Extraer los elementos ref de las líneas coincidentes
                elementos_ref = set()  # Usamos un conjunto para evitar elementos duplicados
                for line in matching_lines:
                    invoke_start_index = line.find(':invoke ref="') + len(':invoke ref="')
                    invoke_end_index = line.find('"', invoke_start_index)
                    invoke_ref = line[invoke_start_index:invoke_end_index]
                    elementos_ref.add(invoke_ref)

                # Imprimir los elementos ref encontrados
                st.success("Elementos ref encontrados en {}: ".format(service))
                for elemento in elementos_ref:
                    st.success(elemento)

                    # Si el elemento contiene '/BusinessServices/', salir del bucle
                    if '/BusinessServices/' in elemento:
                        #st.success(f"elemento: {elemento}")
                        return elemento
                    else:
                        pipeline_path = os.path.join(project_path, elemento + '.pipeline')
                       
            else:
                st.success("El archivo proxy {} no existe.".format(proxy_path))
                break

    return elemento

def extract_xsd_import_paths(wsdl_path):
    xsd_import_paths = set()  # Conjunto para almacenar rutas únicas

    # Leer el contenido del archivo WSDL
    with open(wsdl_path, 'r', encoding='utf-8') as file:
        wsdl_content = file.read()

    # Extraer el contenido dentro de CDATA usando una expresión regular
    cdata_match = re.search(r'<!\[CDATA\[(.*?)\]\]>', wsdl_content, re.DOTALL)
    
    if cdata_match:
        cdata_content = cdata_match.group(1)  # Obtener solo el contenido dentro de CDATA

        # Parsear el contenido XML dentro del CDATA
        try:
            root = ET.fromstring(cdata_content)  # Convertir el CDATA en XML
        except ET.ParseError as e:
            print("Error al parsear el contenido de CDATA:", e)
            return xsd_import_paths

        # Espacios de nombres comunes en WSDL
        namespaces = {
            'xsd': 'http://www.w3.org/2001/XMLSchema'
        }

        # Buscar todos los elementos <xsd:import>
        for xsd_import in root.findall(".//xsd:import", namespaces):
            schema_location = xsd_import.get("schemaLocation")
            if schema_location:
                xsd_import_paths.add(schema_location)
    return list(xsd_import_paths)  # Convertimos el conjunto de vuelta a lista antes de devolverlo

def find_import_elements_with_namespace(xsd_content, target_namespace, xsd_file_path):
    schema_location = ""
    absolute_schema_location = None  # Inicializa la variable

    namespaces = {
        'xsd': 'http://www.w3.org/2001/XMLSchema'
        # Agrega otros namespaces si es necesario
    }
    #st.success(f"target_namespace: {target_namespace}")

    root = ET.fromstring(xsd_content)
    
    #st.success(f"xsd_file_path: {xsd_file_path}")
    
    # Busca todos los elementos import
    xsd_import_elements = root.findall(".//xsd:import", namespaces)

    for import_element in xsd_import_elements:
        namespace = import_element.get('namespace')
        #st.success(f"namespace: {namespace}")
        if namespace == target_namespace:
            schema_location = import_element.get('schemaLocation')
            #st.success(f"Found xsd:import with namespace '{namespace}': {schema_location}")
            
            # Concatena la ruta del archivo XSD principal con la ubicación del esquema importado
            absolute_schema_location = os.path.normpath(os.path.join(os.path.dirname(xsd_file_path), schema_location)).replace('\\', '/')
            #st.success(f"schema_location: {absolute_schema_location}")
            break  # Si encuentras la coincidencia, sal del bucle
    
    return absolute_schema_location  # Esto devolverá None si no se encontró coincidencia "

def extract_namespaces(xsd_content):
    """Extrae los namespaces definidos en el XSD."""
    namespaces = {}
    matches = re.findall(r'xmlns:([\w]+)="([^"]+)"', xsd_content)
    for prefix, uri in matches:
        namespaces[prefix] = uri
    return namespaces


def extract_imports(root):
    """Extrae los imports y los mapea con sus schemaLocation."""
    # Detectar el prefijo correcto para XML Schema (puede ser xs: o xsd:)
    schema_ns = "http://www.w3.org/2001/XMLSchema"
    prefix = None
    
    # Buscar en los atributos del root el namespace correspondiente
    for attr in root.attrib:
        if root.attrib[attr] == schema_ns:
            prefix = attr.split(":")[-1]  # Extraer el prefijo después de "xmlns:"
            break
    
    # Si no se encontró prefijo, usar xs por defecto
    if not prefix:
        prefix = "xs"

    # Buscar los imports con el prefijo detectado
    imports = {}
    for imp in root.findall(f".//{prefix}:import", {prefix: schema_ns}):
        namespace = imp.attrib.get('namespace')
        schema_location = imp.attrib.get('schemaLocation')
        if namespace and schema_location:
            imports[namespace] = schema_location
    
    return imports

def get_correct_xsd_path(current_xsd_path, schema_location):
    """
    Corrige la ruta de un XSD importado considerando los niveles de directorio.
    """
    base_path = os.path.dirname(current_xsd_path)  # Obtener la carpeta del XSD actual
    #st.success(f"base_path: {base_path}")
    corrected_path = os.path.abspath(os.path.join(base_path, schema_location))
    #st.success(f"corrected_path: {corrected_path}")    # Resolver la ruta correcta
    corrected_path = corrected_path.replace("/mount/src/documentacioncompletaosb/extraccion_jar","")
    corrected_path = corrected_path.replace("/mount/src/documentacioncompletaosb","")
    corrected_path = corrected_path.replace(".xsd",".XMLSchema")
    #st.success(f"corrected_path: {corrected_path}")    # Resolver la ruta correcta

    return corrected_path

def parse_xsd_file(project_path, xsd_file_path, operation_name, service_url, capa_proyecto, 
                   operacion_business, operations, service_name, operation_actual, 
                   target_complex_type=None, root_element_name=None,
                   request_elements=None, response_elements=None):
    """
    Parsea un XSD y extrae los elementos request/response de forma recursiva.
    """

    # 🔹 Asegurar que las listas no se reinicien
    if request_elements is None:
        request_elements = []
    if response_elements is None:
        response_elements = []

    extraccion_dir = os.path.abspath(project_path)
    xsd_file_path = os.path.normpath(xsd_file_path.strip("/\\"))  
    subcarpeta_xsd = os.path.dirname(xsd_file_path)
    subcarpeta_xsd = os.path.normpath(subcarpeta_xsd).replace("../", "")

    ruta_corregida = os.path.join(extraccion_dir, subcarpeta_xsd, os.path.basename(xsd_file_path))
    
    #st.success(f"extraccion_dir: {extraccion_dir}")
    #st.success(f"xsd_file_path: {xsd_file_path}")
    #st.success(f"subcarpeta_xsd: {subcarpeta_xsd}")
    #st.success(f"Ruta corregida FINAL: {ruta_corregida}")
    
    if not os.path.isfile(ruta_corregida):
        st.error(f"El archivo XSD {ruta_corregida} no existe.")
        return request_elements, response_elements

    # Leer el contenido del XSD
    with open(ruta_corregida, 'r', encoding="utf-8") as f:
        xsd_content = f.read()

    # Extraer el contenido de CDATA si es necesario
    cdata_match = re.search(r'<!\[CDATA\[(.*?)\]\]>', xsd_content, re.DOTALL)
    if cdata_match:
        xsd_content = cdata_match.group(1)
        #st.success("Se ha extraído el contenido de CDATA correctamente")

    try:
        root = ET.fromstring(xsd_content)
    except ET.ParseError as e:
        st.error(f"Error al analizar el XMLSchema: {e}")
        return request_elements, response_elements

    namespaces = extract_namespaces(xsd_content)
    imports = extract_imports(root)

    #st.success(f"Namespaces detectados: {namespaces}")
    #st.success(f"Imports encontrados: {imports}")

    # 🔹 Verificar qué prefijos están en el namespaces
    valid_prefixes = [p for p in ['xs', 'xsd'] if p in namespaces]

    if not valid_prefixes:
        st.error("⛔ No se encontró un prefijo válido en los namespaces del XSD")
        return request_elements, response_elements  # Salir si no hay prefijos válidos

    # 🔹 Tomar el primer prefijo encontrado en namespaces (xs o xsd)
    prefix = valid_prefixes[0]
    #st.success(f"prefix: {prefix}")

    # 🔹 Buscar complexTypes con el prefijo detectado dinámicamente
    complex_types = {
        elem.attrib.get('name', None): elem
        for elem in root.findall(f".//{prefix}:complexType", namespaces)
        if 'name' in elem.attrib
    }

    # 🔹 Buscar todos los elementos principales con el prefijo detectado
    root_elements = {
        elem.attrib.get('name', ''): elem.attrib.get('type', '').split(':')[-1]
        for elem in root.findall(f".//{prefix}:element", namespaces)
    }

    # 🚀 **Si `target_complex_type` está definido, buscar SOLO ese complexType.**
    if target_complex_type:
        #st.success(f"🔍 Buscando SOLO el complexType: {target_complex_type}")
        explorar_complex_type(target_complex_type, root_element_name, complex_types, namespaces, imports, extraccion_dir, 
                              xsd_file_path, project_path, service_url, capa_proyecto, operacion_business, 
                              operations, service_name, operation_actual, request_elements, response_elements, operation_name)
        return request_elements, response_elements

    # 🔹 Si `target_complex_type` no está, procesamos TODO desde los elementos raíz.
    for root_element_name, complex_type in root_elements.items():
        #st.success(f"Procesando raíz: {root_element_name} -> {complex_type}")

        if complex_type in complex_types:
            explorar_complex_type(complex_type, root_element_name, complex_types, namespaces, imports, extraccion_dir, 
                                  xsd_file_path, project_path, service_url, capa_proyecto, operacion_business, 
                                  operations, service_name, operation_actual, request_elements, response_elements, operation_name)

    #st.success(f"Total elementos request: {len(request_elements)}")
    #st.success(f"Total elementos response: {len(response_elements)}")
    return request_elements, response_elements


def explorar_complex_type(type_name, parent_element_name, complex_types, namespaces, imports, extraccion_dir, 
                          xsd_file_path, project_path, service_url, capa_proyecto, operacion_business, 
                          operations, service_name, operation_actual, request_elements, response_elements, operation_name):
    """Explora recursivamente un complexType y extrae sus elementos internos."""

    type_name = type_name.split(':')[-1]  

    if type_name in complex_types:
        #st.success(f"Explorando complexType: {type_name}")

        # 🔹 Buscar un prefijo válido
        prefix = next((p for p in ['xs', 'xsd'] if p in namespaces), None)
        if not prefix:
            st.error(f"⛔ No se encontró un prefijo válido en namespaces: {namespaces}")
            return
        
        # 🔹 Buscar 'sequence' con prefijo válido
        sequence = complex_types[type_name].find(f'{prefix}:sequence', namespaces)
        if sequence is None:
            #st.warning(f"⚠ No se encontró 'sequence' en {type_name}")
            
            complex_content = complex_types[type_name].find(f'{prefix}:complexContent', namespaces)
            if complex_content is not None:
                extension = complex_content.find(f'{prefix}:extension', namespaces)
                if extension is not None and 'base' in extension.attrib:
                    base_type = extension.attrib['base'].split(":")[-1]  # Obtener el nombre sin prefijo
                    
                    #st.success(f"🔄 {type_name} extiende {base_type}, explorando {base_type}...")
                    explorar_complex_type(base_type, parent_element_name, complex_types, namespaces, imports, 
                                          extraccion_dir, xsd_file_path, project_path, service_url, capa_proyecto, 
                                          operacion_business, operations, service_name, operation_actual, 
                                          request_elements, response_elements, operation_name)
                    return  # Salimos porque ya delegamos la exploración a la base
                
            st.warning(f"⚠ No se encontró ni 'sequence' ni 'extension' en {type_name}")
            return  # Si no hay ni sequence ni extensión, no hay nada más que hacer

        #st.success(f"Usando prefijo: {prefix}")

        if prefix not in namespaces:
            st.error(f"⛔ Error: el prefijo '{prefix}' no está en namespaces: {namespaces}")
            return

        for element in sequence.findall(f'{prefix}:element', namespaces):
            element_name = element.attrib.get('name', '')
            element_type = element.attrib.get('type', '')
            element_minOccurs = element.attrib.get('minOccurs', '')
            if element_minOccurs is None:
                element_minOccurs = 0
           
            #st.success(f"element_name: {element_name}")
            #st.success(f"element_type: {element_type}")
            #st.success(f"element_minOccurs: {element_minOccurs}")
            full_name = f"{parent_element_name}.{element_name}" if parent_element_name else element_name
            #st.success(f"Encontrado elemento: {full_name} con tipo: {element_type} y minOcurs: {element_minOccurs}")

            # 🔹 Buscar 'simpleType' con prefijo válido
            simple_type = element.find(f'{prefix}:simpleType', namespaces)
            if simple_type is not None:
                restriction = simple_type.find(f'{prefix}:restriction', namespaces)
                if restriction is not None and 'base' in restriction.attrib:
                    element_type = restriction.attrib['base']
                    #st.success(f"Elemento {full_name} tiene restricción con base: {element_type}")

            if element_type.startswith(("xsd:", "xs:")):
                element_details = {
                    'elemento': parent_element_name.split('.')[0],  
                    'name': full_name,  
                    'type': element_type,
                    'url': service_url,
                    'ruta': capa_proyecto,
                    'minOccurs': element_minOccurs,
                    'operations': operations,
                    'service_name': service_name,
                    'operation_actual': operation_actual,
                }
                #st.success(f"Agregando elemento primitivo: {element_details}")

                if 'Request' in parent_element_name:
                    request_elements.append(element_details)
                elif 'Response' in parent_element_name:
                    response_elements.append(element_details)

            elif element_type in complex_types:
                #st.success(f"Buscando {element_type} en el mismo XSD")
                explorar_complex_type(element_type, full_name, complex_types, namespaces, imports, extraccion_dir, 
                                      xsd_file_path, project_path, service_url, capa_proyecto, operacion_business, 
                                      operations, service_name, operation_actual, request_elements, response_elements, operation_name)

            elif ':' in element_type:
                prefix, nested_type = element_type.split(':')
                
                if nested_type in complex_types:
                    #st.success(f"Buscando {nested_type} en el mismo XSD")
                    explorar_complex_type(nested_type, full_name, complex_types, namespaces, imports, extraccion_dir, 
                                          xsd_file_path, project_path, service_url, capa_proyecto, operacion_business, 
                                          operations, service_name, operation_actual, request_elements, response_elements, operation_name)
                elif prefix in namespaces:
                    namespace = namespaces[prefix]
                    if namespace in imports:
                        schema_location = imports[namespace]
                        #st.warning(f"El tipo {nested_type} está en otro XSD: {schema_location}")
                        corrected_xsd_path = get_correct_xsd_path(xsd_file_path, schema_location)
                        #st.success(f"corrected_xsd_path: {corrected_xsd_path}")
                        new_xsd_path = os.path.join(extraccion_dir, corrected_xsd_path)
                        #st.success(f"new_xsd_path: {new_xsd_path}")

                        parse_xsd_file(project_path, new_xsd_path, operation_name, service_url, 
                                       capa_proyecto, operacion_business, operations, 
                                       service_name, operation_actual, 
                                       target_complex_type=nested_type, 
                                       root_element_name=full_name,
                                       request_elements=request_elements,
                                       response_elements=response_elements)
                    else:
                        st.warning(f"No se encontró el namespace para el prefijo {prefix}")
                else:
                    st.warning(f"complexType {element_type} no encontrado en el XSD")
    else:
        st.warning(f"complexType {type_name} no encontrado en el XSD")

def leer_xsd_file(xsd_file_path, complexType_name):
    elements_list = []

    if xsd_file_path.endswith('.xsd') and os.path.isfile(xsd_file_path):
        with open(xsd_file_path, 'r', encoding="utf-8") as f:
            xsd_content = f.read()
            root = ET.fromstring(xsd_content)
            namespaces = {'xs': 'http://www.w3.org/2001/XMLSchema'}
            
            #st.success(f"xsd_file_path: {xsd_file_path}")
            

            # Función para detectar y eliminar repeticiones cíclicas en los nombres de los elementos
            def remove_repetitions(element_name):
                parts = element_name.split('.')
                seen = set()
                unique_parts = []
                for part in parts:
                    if part in seen:
                        break
                    seen.add(part)
                    unique_parts.append(part)
                return '.'.join(unique_parts)

            # Función para obtener elementos recursivamente con control de visitas
            def get_elements(complex_type_element, parent_name, visited):
                sequence_element = complex_type_element.find('xs:sequence', namespaces)
                if sequence_element is not None:
                    child_elements = sequence_element.findall('xs:element', namespaces)
                    for child_element in child_elements:
                        element_name = child_element.attrib.get('name', '')
                        element_type = child_element.attrib.get('type', '')
                        full_element_name = f"{parent_name}.{element_name}"

                        # Detectar y eliminar repeticiones cíclicas
                        full_element_name = remove_repetitions(full_element_name)

                        #st.success(f"element_name: {full_element_name}")
                        #st.success(f"element_type: {element_type}")
                        if not element_type:
                            element_type = 'xs:string'
                        elements_list.append({'element_name': full_element_name, 'element_type': element_type})

                        if ':' in element_type:
                            prefix, complexType_name_interno = element_type.split(':')
                            if complexType_name_interno not in visited:
                                visited.add(complexType_name_interno)
                                complex_type_element = root.find(f".//xs:complexType[@name='{complexType_name_interno}']", namespaces)
                                if complex_type_element is not None:
                                    get_elements(complex_type_element, full_element_name, visited)

            complex_type_element = root.find(f".//xs:complexType[@name='{complexType_name}']", namespaces)
            if complex_type_element is not None:
                
                #st.success(f"complex_type_name: {complexType_name}")
                
                #st.success(f"complex_type_element: {complex_type_element}")
                
                
                visited = set()
                get_elements(complex_type_element, complexType_name, visited)
                
    return elements_list
    
def has_http_provider_id(xml_content):
    root = ET.fromstring(xml_content)
    namespaces = {'tran': 'http://www.bea.com/wli/sb/transports'}
    provider_id_element = root.find(".//tran:provider-id", namespaces)
    return provider_id_element is not None and provider_id_element.text == 'http'

def extract_project_name_from_proxy(proxy_path):
    try:
        with open(proxy_path, 'r', encoding="utf-8") as f:
            content = f.read()
            start = content.find('<con:wsdl ref="') + len('<con:wsdl ref="')
            end = content.find('"', start)
            wsdl_ref = content[start:end]
            return wsdl_ref.split("/")[0]
    except FileNotFoundError:
        ##st.success(f"El archivo {proxy_path} no existe.")
        return None

def reemplazar_texto_en_doc(doc, reemplazos):
    """
    Reemplaza variables en el documento, incluyendo encabezados, pies de página y contenido.
    """
    # Reemplazo en párrafos normales
    for parrafo in doc.paragraphs:
        for clave, valor in reemplazos.items():
            if clave in parrafo.text:
                parrafo.text = parrafo.text.replace(clave, valor)
    
    # Reemplazo en encabezados y pies de página
    for section in doc.sections:
        # Encabezado
        for parrafo in section.header.paragraphs:
            for clave, valor in reemplazos.items():
                if clave in parrafo.text:
                    parrafo.text = parrafo.text.replace(clave, valor)
        
        # Pie de página
        for parrafo in section.footer.paragraphs:
            for clave, valor in reemplazos.items():
                if clave in parrafo.text:
                    parrafo.text = parrafo.text.replace(clave, valor)
    
    # Reemplazo en tablas sin alterar el formato
    for tabla in doc.tables:
        for fila in tabla.rows:
            for celda in fila.cells:
                for clave, valor in reemplazos.items():
                    if clave in celda.text:
                        celda.text = celda.text.replace(clave, valor)
    
    return doc

def extract_service_url(xml_content):
    root = ET.fromstring(xml_content)
    tran_namespace = {'tran': 'http://www.bea.com/wli/sb/transports', 'env': 'http://www.bea.com/wli/config/env'}
    uri_element = root.find(".//tran:URI/env:value", namespaces=tran_namespace)
    if uri_element is not None:
        return uri_element.text
    return ''

def extract_pipeline_path_from_proxy(proxy_path, jdeveloper_projects_dir):
    try:
        with open(proxy_path, 'r', encoding="utf-8") as f:
            content = f.read()
            start = content.find('<ser:invoke ref="') + len('<ser:invoke ref="')
            end = content.find('"', start)
            pipeline_ref = content[start:end]
            pipeline_path = os.path.join(jdeveloper_projects_dir, pipeline_ref + ".Pipeline")
            return pipeline_path
    except FileNotFoundError:
        print(f"El archivo {proxy_path} no pudo ser encontrado.")
        return None  # O puedes lanzar otra excepción, dependiendo del flujo de tu programa.
     
def extract_wsdl_relative_path(xml_content):
    root = ET.fromstring(xml_content)
    namespaces = {'con': 'http://www.bea.com/wli/sb/services/bindings/config'}
    wsdl_ref_element = root.find(".//con:wsdl", namespaces)
    if wsdl_ref_element is not None:
        wsdl_relative_path = wsdl_ref_element.attrib.get('ref', '')
        return wsdl_relative_path
    return ''
    
def extract_wsdl_operations(wsdl_path):
    operations = set()  # Utilizamos un conjunto en lugar de una lista
    if wsdl_path.endswith('.WSDL') and os.path.isfile(wsdl_path):
        with open(wsdl_path, 'r', encoding="utf-8") as f:
            wsdl_content = f.read()
            # Buscamos todas las coincidencias de "<operation name=" seguidas por el nombre de la operación
            operation_names = re.findall(r'operation name="([^"]+)', wsdl_content)
            for operation_name in operation_names:
                operations.add(operation_name)  # Agregamos el nombre de la operación al conjunto
    return list(operations)  # Convertimos el conjunto de vuelta a lista antes de devolverlo

def buscar_definicion_audibpel(branch_element, operation_name, namespaces, root):
    response_element = branch_element.find(".//con:response", namespaces)
    valor_nombre_flujo= operation_name
    if response_element is not None:
        response_value = response_element.text
        st.success(f"El valor del elemento <con:response> dentro de branch_element es: {response_value}")

        pipelines = root.findall(".//con:pipeline[@name='" + response_value + "']", namespaces)

        for pipeline in pipelines:
            print("Se encontró un pipeline con name igual a '{}':".format(response_value))
            
            service_elements = pipeline.findall(".//con2:xqueryTransform", namespaces)
            st.success(f"service_elements: {service_elements}")

            for service_element in service_elements:
            
                param_element = service_element.find(".//con2:param[@name='nombreFlujo']", namespaces)
                st.success(f"param_element: {param_element}")

                if param_element is not None:
                    valor_nombre_flujo = param_element.find("./con2:path", namespaces).text
                    st.success(valor_nombre_flujo)
                    
                    valor_nombre_flujo = valor_nombre_flujo.replace('"', '')
                    
                    valor_nombre_flujo = valor_nombre_flujo.replace("'", "")
                    
                    valor_nombre_flujo = valor_nombre_flujo.replace(',', '')

                    valor_nombre_flujo = valor_nombre_flujo.replace('fn:concat', '')
                    
                    valor_nombre_flujo = valor_nombre_flujo.replace('concat', '')
                    
                    valor_nombre_flujo = valor_nombre_flujo.replace('data', '')
                    
                    valor_nombre_flujo = valor_nombre_flujo.replace('fn:data', '')
                    
                    valor_nombre_flujo = valor_nombre_flujo.replace('(', '')
                    
                    valor_nombre_flujo = valor_nombre_flujo.replace(')', '')

                    variables_a_reemplazar = ['$operacionExp', '$operacionAbc', '$operacionEXP', '$operacionABC', '$operation']
                    for variable in variables_a_reemplazar:
                        valor_nombre_flujo = valor_nombre_flujo.replace(variable, operation_name)
            
    st.success(valor_nombre_flujo)
    return valor_nombre_flujo

def extract_service_for_operations_audibpel(pipeline_path, operations):
    services_for_operations = {}
    seguir = True
    
    st.success("***************************** INICIO EXTRACT SERVICE OPERATIONS*********************************************")
        
    if not os.path.exists(pipeline_path):
        st.error(f"El archivo no existe: {pipeline_path}")
    elif not os.path.isfile(pipeline_path):
        st.error(f"No es un archivo válido: {pipeline_path}")
    
    if pipeline_path.endswith('.pipeline') and os.path.isfile(pipeline_path):
        st.success(f"pipeline_path: {pipeline_path}")
        with open(pipeline_path, 'r', encoding="utf-8") as f:
            pipeline_content = f.read()
            root = ET.fromstring(pipeline_content)
            namespaces = {'con': 'http://www.bea.com/wli/sb/pipeline/config', 
                          'con1': 'http://www.bea.com/wli/sb/stages/routing/config',
                          'con2': 'http://www.bea.com/wli/sb/stages/config',
                          'con3': 'http://www.bea.com/wli/sb/stages/transform/config',
                          'con4': 'http://www.bea.com/wli/sb/stages/publish/config',
                          'ref': 'http://www.bea.com/wli/sb/reference',
                          'xsi': 'http://www.w3.org/2001/XMLSchema-instance'} 
                          

            st.success(f"LEYENDO ROOT OPERATIONS AUDIBPEL: {root}")
            # Parsea el archivo .pipeline
            tree = ET.parse(pipeline_path)
            root = tree.getroot()

            branch_elements = root.findall(".//con:branch", namespaces)
            if branch_elements:
                for branch_element in branch_elements:
                    
                    operation_name = branch_element.attrib.get('name', '')
                    
                    st.success(f"Operation Name Branch Elements: {operation_name}")
                    if operation_name in operations:
                        service_element = branch_element.find(".//con1:service", namespaces)
                        st.success(f"service_element: {service_element}")
                        
                                    
                        if service_element is not None:                            
                            #Consulta audibpel:
                            st.success("buscar_definicion_audibpel")
                            nombre_audibpel = buscar_definicion_audibpel(branch_element,operation_name,namespaces,root)
                            st.success(f"nombre_audibpel: {nombre_audibpel}")
                            
                            service_ref = service_element.attrib.get('ref', '')
                            services_for_operations.setdefault(operation_name, []).append((service_ref, nombre_audibpel))
                            st.success("branch_elements")
                            st.success(f"Operation Name: {operation_name}, Service Ref: {service_ref}, nombre_audibpel: {nombre_audibpel}")
                            
                            st.success(services_for_operations)
                            
                            seguir = False
                            continue
                        else:
                            seguir = True
                            #Consulta audibpel:
                            st.success("buscar_definicion_audibpel")
                            nombre_audibpel = buscar_definicion_audibpel(branch_element,operation_name,namespaces,root)
                            st.success(f"nombre_audibpel: {nombre_audibpel}")
                            
                            # Si service_element es None, buscar el elemento <con:request> dentro de branch_element
                            request_element = branch_element.find(".//con:request", namespaces)
                            st.success(f"request_element: {request_element}")
                            if request_element is not None:
                                request_value = request_element.text
                                print("El valor del elemento <con:request> dentro de branch_element es:", request_value)
                                
                                
                                # Utilizamos XPath para encontrar los elementos 'con:pipeline' con el atributo 'name' igual a 'request_value'
                                pipelines = root.findall(".//con:pipeline[@name='" + request_value + "']", namespaces)

                                # Imprimimos los elementos encontrados (si los hay)
                                for pipeline in pipelines:
                                    print("Se encontró un pipeline con name igual a '{}':".format(request_value))
                                    #print(ET.tostring(pipeline, encoding='unicode'))
                                    
                                    ns_stage_transform_config   = {'con1': 'http://www.bea.com/wli/sb/stages/transform/config'}
                                    ns_stage_publish_config     = {'con1': 'http://www.bea.com/wli/sb/stages/publish/config'}
                                    ns_stage_routing_config     = {'con1': 'http://www.bea.com/wli/sb/stages/routing/config'}
                                    ns_stage_config             = {'con1':'http://www.bea.com/wli/sb/stages/config'}
                                    
                                    ns_stage_pipeline_config    = {'con': 'http://www.bea.com/wli/sb/pipeline/config',
                                                                'con1': 'http://www.bea.com/wli/sb/stages/routing/config',
                                                                'con2': 'http://www.bea.com/wli/sb/stages/config',
                                                                'con3': 'http://www.bea.com/wli/sb/stages/transform/config',
                                                                'ref': 'http://www.bea.com/wli/sb/reference',
                                                                'xsi': 'http://www.w3.org/2001/XMLSchema-instance'}
                                    
                                    ns                           = {'con': 'http://www.example.com',
                                                                    'con4': 'http://www.bea.com/wli/sb/stages/routing/config',
                                                                    'xsi': 'http://www.w3.org/2001/XMLSchema-instance'}
                                    

                                    ws_callouts = pipeline.findall(".//con1:wsCallout", namespaces=ns_stage_transform_config)
                                    #st.success(f"ws_callouts: {ws_callouts}")
                                    java_callouts = pipeline.findall(".//con1:javaCallout", namespaces=ns_stage_transform_config)
                                    #st.success(f"java_callouts: {java_callouts}")
                                    routes = pipeline.findall(".//con1:route", namespaces=ns_stage_publish_config)
                                    #st.success(f"routes: {routes}")
                                    routes2 = pipeline.findall(".//con1:route", namespaces=ns_stage_routing_config)
                                    #st.success(f"routes2: {routes2}")
                                    flow_elements = pipeline.findall(".//con:flow", ns_stage_pipeline_config)
                                    #st.success(f"flow_elements: {flow_elements}")
                                    
                                    
                                    for ws_callout in ws_callouts:
                                        service_element = ws_callout.find(".//con1:service", namespaces=ns_stage_transform_config)
                                        operation_element = ws_callout.find(".//con1:operation", namespaces=ns_stage_transform_config)
                                        if service_element is not None and operation_element is not None:
                                            service_ref = service_element.attrib.get('ref', '')
                                            services_for_operations.setdefault(operation_name, []).append((service_ref, nombre_audibpel))
                                            st.success(f"services_for_operations ws_callouts: {services_for_operations}")
                                            seguir = False
                                            continue
                                    
                                    
                                    for java_callout in java_callouts:
                                        method_element = java_callout.find(".//con1:method", namespaces=ns_stage_transform_config)
                                        if method_element is not None:
                                            method_text = method_element.text
                                            service_element = java_callout.find(".//con1:archive", namespaces=ns_stage_transform_config)
                                            if service_element is not None:
                                                service_ref = service_element.attrib.get('ref', '')
                                                services_for_operations.setdefault(operation_name, []).append((service_ref, nombre_audibpel))
                                                st.success(f"services_for_operations java_callouts: {services_for_operations}")
                                                seguir = False
                                                continue

                                    for route in routes:
                                        service_element = route.find(".//con1:service", namespaces=ns_stage_publish_config)
                                        operation_element = route.find(".//con1:operation", namespaces=ns_stage_publish_config)
                                        if service_element is not None and operation_element is not None:
                                            service_ref = service_element.attrib.get('ref', '')
                                            services_for_operations.setdefault(operation_name, []).append((service_ref, nombre_audibpel))
                                            st.success(f"services_for_operations routes: {services_for_operations}")
                                            seguir = False
                                            continue
                                    
                                    for route in routes2:
                                        service_element = route.find(" .//con1:service", namespaces=ns_stage_routing_config)
                                        operation_element = route.find(" .//con1:operation", namespaces=ns_stage_routing_config)
                                        if service_element is not None and operation_element is not None:
                                            service_ref = service_element.attrib.get('ref', '')
                                            services_for_operations.setdefault(operation_name, []).append((service_ref, nombre_audibpel))
                                            st.success(f"services_for_operations routes2: {services_for_operations}")
                                            seguir = False
                                            continue
                                            
                                     
                                     # Itera sobre cada elemento <con:flow> encontrado
                                    for flow_element in flow_elements:
                                        # Encuentra todos los elementos <con1:service> dentro de <con:flow>
                                        service_elements = flow_element.findall(".//con1:service[@xsi:type='ref:BusinessServiceRef']", ns_stage_pipeline_config)
                                        
                                        # Si no se encuentra ningún servicio dentro del flujo, salta al siguiente flujo
                                        if not service_elements:
                                            seguir = False
                                            continue
                                        
                                        # Itera sobre cada elemento <con1:service> encontrado dentro de <con:flow>
                                        for service_element in service_elements:
                                            # Accede al atributo 'ref' del elemento <con1:service>
                                            service_ref = service_element.attrib.get('ref', '')

                                            # Encuentra todos los elementos <con1:operation> dentro de <con:flow>
                                            operation_elements = flow_element.findall(".//con1:operation", ns_stage_pipeline_config)


                                            operation_element = operation_elements[0]

                                            # Agrega la relación entre el nombre de la operación y la referencia del servicio al diccionario services_for_operations
                                            services_for_operations.setdefault(operation_name, []).append((service_ref, nombre_audibpel))
                                            seguir = False
                                            continue
                                                    
                            st.success(services_for_operations)
                            




            if seguir:
                flow_elements = root.findall(".//con:flow", namespaces)

                
                for flow_element in flow_elements:
                    
                    service_elements = flow_element.findall(".//con1:service[@xsi:type='ref:BusinessServiceRef']", namespaces)
                    proxy_elements = flow_element.findall(".//con1:service[@xsi:type='ref:ProxyRef']", namespaces)
                    
                    for service_element in service_elements:
                        service_ref = service_element.attrib.get('ref', '')
                        operation_elements = flow_element.findall(".//con1:operation", namespaces)
                        for operation_element in operation_elements:
                            operation_name = operation_element.text.strip()
                            st.success(f"Operation Name: {operation_name}")
                            st.success(f"len(operations): {len(operations)}")
                            
                            if len(operations) == 1:
                                operation_name = operations[0]
                                
                            st.success(f"Operation Name: {operation_name}")
                            
                            if operation_name in operations:
                                #Consulta audibpel:
                                st.success("buscar_definicion_audibpel")
                                nombre_audibpel = buscar_definicion_audibpel(flow_element,operation_name,namespaces,root)
                                st.success(f"nombre_audibpel: {nombre_audibpel}")
                                services_for_operations.setdefault(operation_name, []).append((service_ref, nombre_audibpel))
                                st.success("flow_element")
                                st.success(f"Operation Name: {operation_name}")
                                
                                seguir = False
                                continue
                    
                    for proxy_element in proxy_elements:
                        service_ref = proxy_element.attrib.get('ref', '')
                        operation_elements = flow_element.findall(".//con1:operation", namespaces)
                        for operation_element in operation_elements:
                            
                            operation_name = operation_element.text.strip()
                            st.success(f"Operation Name: {operation_name}")
                            st.success(f"len(operations): {len(operations)}")
                            
                            if len(operations) == 1:
                                operation_name = operations[0]
                                
                            st.success(f"Operation Name: {operation_name}")
                            
                            if operation_name in operations:
                                #Consulta audibpel:
                                st.success("buscar_definicion_audibpel")
                                nombre_audibpel = buscar_definicion_audibpel(flow_element,operation_name,namespaces,root)
                                st.success(f"nombre_audibpel: {nombre_audibpel}")
                                services_for_operations.setdefault(operation_name, []).append((service_ref, nombre_audibpel))
                                st.success("flow_element")
                                st.success(f"Operation Name: {operation_name}")
                                
                                seguir = False
                                continue
                            
                
            if seguir:               
                route_elements = root.findall(".//con:route-node", namespaces)
                for route_element in route_elements:
                    operation_element = route_element.find(".//con1:operation", namespaces)
                    if operation_element is not None:
                        operation_name = operation_element.text.strip()  
                        if operation_name in operations:
                            service_element = route_element.find(".//con1:service", namespaces)
                            if service_element is not None:
                                service_ref = service_element.attrib.get('ref', '')
                                services_for_operations.setdefault(operation_name, []).append((service_ref, 'N/A'))
                                st.success("route_elements")
                                st.success(f"Operation Name: {operation_name}, Service Ref: {service_ref}")
                                
                                seguir = False
                                continue
                                
                # Encuentra todos los elementos <wsCallout> sin importar el prefijo del namespace
                callout_elements = [element for element in root.iter() if element.tag.endswith('wsCallout')]
                
                # Itera sobre cada elemento <wsCallout> encontrado
                for callout_element in callout_elements:
                    operation_name = ""
                    service_ref = ""
                    operation_element = callout_element.find(".//con3:operation", namespaces)
                    if operation_element is not None:
                        operation_name = operation_element.text.strip()
                    service_element = callout_element.find(".//con3:service", namespaces)
                    if service_element is not None:
                        service_ref = service_element.attrib.get('ref', '')
                    if operation_name and service_ref:
                        services_for_operations.setdefault(operation_name, []).append((service_ref, 'N/A'))
                        st.success("callout_element")
                        st.success(f"Operation Name: {operation_name}, Service Ref: {service_ref}")
                        
                        seguir = False
                        continue
                                
    st.success(f"SERVICES FOR: {services_for_operations}")
    st.success("***************************** FIN EXTRACT SERVICE OPERATIONS*********************************************")
    
    return services_for_operations

def extraer_operaciones_expuestas_http(project_path):
    wsdl_operations_map = {}
    for root, dirs, files in os.walk(project_path):
        if os.path.basename(root) == "Proxies":
            ##st.success(f"✅ Proxies {elementos_xsd}")
            for file in files:
                if file.endswith('.ProxyService'):
                    osb_file_path = os.path.join(root, file)
                    #st.success(f"✅ osb_file_path {osb_file_path}")
                    project_name = extract_project_name_from_proxy(osb_file_path)
                    
                    if project_name is None:
                        continue 
                    pipeline_path = extract_pipeline_path_from_proxy(osb_file_path, project_path)
                    ##st.success(f"✅ pipeline_path {pipeline_path}")
                    with open(osb_file_path, 'r', encoding="utf-8") as f:
                        content = f.read()
                        if has_http_provider_id(content):
                            service_name = os.path.splitext(file)[0]
                            st.success(f"✅ project_name {project_name}")
                            st.success(f"✅ service_name {service_name}")
                            service_url = extract_service_url(content)
                            st.success(f"✅ service_url {service_url}")
                            wsdl_relative_path = extract_wsdl_relative_path(content)
                            if wsdl_relative_path:
                                wsdl_path = os.path.join(project_path, wsdl_relative_path + ".WSDL")
                                capa_proyecto = '/'+ wsdl_relative_path.split('/')[0]
                                
                                st.success(f"capa_proyecto: {capa_proyecto}")
                                
                                st.success(f"wsdl_path: {wsdl_path}")
                                operations = extract_wsdl_operations(wsdl_path)
                                wsdl_operations_map[wsdl_path] = (
                                    operations, project_name, service_name, pipeline_path,service_url, capa_proyecto
                                )
    st.success(f"✅ wsdl_operations_map {wsdl_operations_map}")
    return wsdl_operations_map

def extraer_schemas_operaciones_expuestas_http(project_path,operacion_a_documentar):
    
    osb_services = []
    elementos_xsd = []
    operations =[]
    operation_to_xsd = {}
    found = False  # Variable para rastrear si se encuentra la operación
    
    wsdl_operations_map = extraer_operaciones_expuestas_http(project_path)
    
    # Recorriendo el diccionario
    for wsdl_path, data in wsdl_operations_map.items():
        # Desempaquetar la tupla
        operations, project_name, service_name, pipeline_path, service_url, capa_proyecto = data
        
        st.success(f"wsdl_path: {wsdl_path}")
        st.success(f"operations: {operations}")
        st.success(f"project_name: {project_name}")
        st.success(f"service_name: {service_name}")
        st.success(f"pipeline_path: {pipeline_path}")
        st.success(f"service_url: {service_url}")
        st.success(f"capa_proyecto: {capa_proyecto}")

        imports = extract_xsd_import_paths(wsdl_path)
        #st.success(f"wsdl_path: {wsdl_path}")
        #st.success(f"imports: {imports}")
        
        #st.success(f"project_path: {project_path}")
        # 🔹 Eliminar 'extraccion_jar/' para obtener la ruta relativa base
        wsdl_relative_base = os.path.relpath(wsdl_path, "extraccion_jar")
        #st.success(f"wsdl_relative_base: {wsdl_relative_base}")
        operacion_business = ""
        # 🔹 Obtener la carpeta donde está el WSDL
        wsdl_dir = os.path.dirname(wsdl_relative_base)
        #st.success(f"wsdl_dir: {wsdl_dir}")
        # 🔹 Procesar cada import y ajustar solo los que empiezan con "../Schemas"
        xsd_relative_paths = []
        # 🔹 Modificar `imports` en su lugar
        for i, imp in enumerate(imports):
            if imp.startswith("../Schemas"):  # Solo modificar los que empiezan con "../Schemas"
                imports[i] = os.path.normpath(os.path.join(wsdl_dir, imp))  # Reemplazar en la misma lista
                                            
        
        #st.success(f"imports despues: {imports}")
        
        if operacion_a_documentar in operations or not operacion_a_documentar:
            for operation in operations:
                for xsd in imports:
                    xsd_filename = os.path.basename(xsd).lower()  # Obtener solo el nombre del archivo XSD

                    # 🔹 Buscar coincidencia exacta con el nombre del XSD
                    if xsd_filename == operation.lower() + ".xsd":
                        operation_to_xsd[operation] = xsd
                        break  # Detener la búsqueda cuando encuentra la coincidencia exacta

                else:  # Solo ejecuta este bloque si el `for xsd in imports` no encontró nada
                    xsd_names = [os.path.basename(x).lower() for x in imports]  # Lista de nombres de archivos XSD
                    closest_match = difflib.get_close_matches(operation.lower() + ".xsd", xsd_names, n=1, cutoff=0.7)

                    if closest_match:
                        matched_xsd = next(x for x in imports if os.path.basename(x).lower() == closest_match[0])
                        operation_to_xsd[operation] = matched_xsd
                    else:
                        operation_to_xsd[operation] = None  # No se encontró una coincidencia
            
            #st.success(f"operation_to_xsd: {operation_to_xsd}")
            
            # ✅ Si el usuario especificó una operación, verificar si existe en operation_to_xsd
            if operacion_a_documentar and operacion_a_documentar not in operation_to_xsd:
                continue
            else:
                found = True  # La operación se encontró en este archivo
                # Iterar sobre el diccionario y realizar la llamada a parse_xsd_file
                for operation_name, xsd in operation_to_xsd.items():
                    #
                    operation_actual = operation_name
                    #st.success(f"operation_actual: {operation_actual}")
                    #st.success(f"operacion_a_documentar: {operacion_a_documentar}")
                    if not operacion_a_documentar or operation_name == operacion_a_documentar:
                        #st.success(f"operation_actual: {operation_actual}")
                        st.success(f"🔍 Analizando operacion: {operation_actual}")
                        #st.success(f"service_name: {service_name}")
                        #st.success(f"operation_name: {operation_name}")
                        #st.success(f"service_url: {service_url}")
                        #st.success(f"capa_proyecto: {capa_proyecto}")
                        #st.success(f"operacion_business: {operacion_business}")
                        xsd = os.path.splitext(xsd)[0] + ".XMLSchema"
                        #
                        #
                        #st.success(f"xsd: {xsd}")
                    
                        elementos_xsd = parse_xsd_file(project_path,xsd, operation_name,service_url,capa_proyecto,operacion_business,operations, service_name, operation_actual)
                        #st.success(f"elementos_xsd: {elementos_xsd}")
                        #elementos_completos = list(elementos_xsd) + list(operations) + [operation_actual]
                        osb_services.append(elementos_xsd)
                        
                        osb_services = recorrer_y_extraer_operaciones_servicios_osb(project_path,operacion_a_documentar,operations,pipeline_path)
                    
                        if operacion_a_documentar:
                            return osb_services
                                                    
        if not found:  
            st.error("⛔ No se encuentra la operación en el .jar ⛔")

    #st.success(f"osb_services: {osb_services}")
    return osb_services

def extract_pipeline_path_from_proxy(proxy_path, jdeveloper_projects_dir):
    try:
        with open(proxy_path, 'r', encoding="utf-8") as f:
            content = f.read()
            start = content.find('<ser:invoke ref="') + len('<ser:invoke ref="')
            end = content.find('"', start)
            pipeline_ref = content[start:end]
            pipeline_path = os.path.join(jdeveloper_projects_dir, pipeline_ref + ".pipeline")
            return pipeline_path
    except FileNotFoundError:
        print(f"El archivo {proxy_path} no pudo ser encontrado.")
        return None  # O puedes lanzar otra excepción, dependiendo del flujo de tu programa.

def extract_service_refs_from_pipeline(pipeline_path):
    service_refs = set()  
    try:
        with open(pipeline_path, 'r', encoding="utf-8") as f:
            pipeline_content = f.read()
            root = ET.fromstring(pipeline_content)
            ns = {'con3': 'http://www.bea.com/wli/sb/stages/transform/config',
                  'con2': 'http://www.bea.com/wli/sb/stages/transform/config',
                  'con4': 'http://www.bea.com/wli/sb/stages/publish/config',
                  'con1': 'http://www.bea.com/wli/sb/stages/routing/config'}
            ws_callouts = root.findall(".//con3:wsCallout", namespaces=ns)
            java_callouts = root.findall(".//con2:javaCallout", namespaces=ns)
            routes = root.findall(".//con4:route", namespaces=ns)
            routes2 = root.findall(".//con1:route", namespaces=ns)
            for java_callout in java_callouts:
                archive_element = java_callout.find(".//con2:archive", namespaces=ns)
                if archive_element is not None:
                    archive_ref = archive_element.attrib.get('ref', '')
                    service_refs.add(archive_ref) 
            for ws_callout in ws_callouts:
                service_element = ws_callout.find(".//con3:service", namespaces=ns)
                if service_element is not None:
                    service_ref = service_element.attrib.get('ref', '')
                    service_refs.add(service_ref)
            
            for element in root.iter():
                if element.tag.endswith('wsCallout'):
                    service_element = element.find(".//service")
                    if service_element is not None:
                        service_ref = service_element.attrib.get('ref', '')
                        service_refs.add(service_ref)
            
            
            for route in routes:
                service_element = route.find(".//con4:service", namespaces=ns)
                if service_element is not None:
                    service_ref = service_element.attrib.get('ref', '')
                    service_refs.add(service_ref)
            for route in routes2:
                service_element = route.find(".//con1:service", namespaces=ns)
                if service_element is not None:
                    service_ref = service_element.attrib.get('ref', '')
                    service_refs.add(service_ref)
        return list(service_refs)
    except FileNotFoundError:
        print(f"El archivo {pipeline_path} no se encontró.")
        return []
    except Exception as e:
        print(f"Ocurrió un error al procesar el archivo {pipeline_path}: {e}")
        return []

def extract_service_for_operations(pipeline_path, operations):
    services_for_operations = {}
    
    st.success("***************************** INICIO EXTRACT SERVICE OPERATIONS*********************************************")
    if pipeline_path.endswith('.pipeline') and os.path.isfile(pipeline_path):
        st.success(f"pipeline_path: {pipeline_path}")
        with open(pipeline_path, 'r', encoding="utf-8") as f:
            pipeline_content = f.read()
            
            st.success(pipeline_content)  # Imprime los primeros 500 caracteres
            root = ET.fromstring(pipeline_content)
            namespaces = {'con': 'http://www.bea.com/wli/sb/pipeline/config', 
                          'con1': 'http://www.bea.com/wli/sb/stages/routing/config',
                          'con2': 'http://www.bea.com/wli/sb/stages/config',
                          'con3': 'http://www.bea.com/wli/sb/stages/transform/config',
                          'con4': 'http://www.bea.com/wli/sb/stages/publish/config',                                                          
                          'ref': 'http://www.bea.com/wli/sb/reference',
                          'xsi': 'http://www.w3.org/2001/XMLSchema-instance'} 
                          

            st.success(f"LEYENDO ROOT: {root}")
            # Parsea el archivo .pipeline
            tree = ET.parse(pipeline_path)
            root = tree.getroot()
            root2 = ET.fromstring(pipeline_content)
            
            flow_elements = root.findall(".//con:flow", namespaces)

            
            for flow_element in flow_elements:
                
                service_elements = flow_element.findall(".//con1:service[@xsi:type='ref:BusinessServiceRef']", namespaces)
                proxy_elements = flow_element.findall(".//con1:service[@xsi:type='ref:ProxyRef']", namespaces)
                
                                                                                          
                for service_element in service_elements:
                                                                          
                    service_ref = service_element.attrib.get('ref', '')
                    
                                                                                         
                    operation_elements = flow_element.findall(".//con1:operation", namespaces)
                    for operation_element in operation_elements:
                        operation_name = operation_element.text.strip()
                        services_for_operations[operation_name] = (service_ref)
                        st.success("flow_element")
                        st.success(f"Operation Name: {operation_name}")
                        
                
                for proxy_element in proxy_elements:
                    service_ref = proxy_element.attrib.get('ref', '')
                    operation_elements = flow_element.findall(".//con1:operation", namespaces)
                    for operation_element in operation_elements:
                                                                                                           
                        operation_name = operation_element.text.strip()
                                                                                                                                                  
                        services_for_operations[operation_name] = service_ref
                                                                                
                        st.success("flow_element")
                        st.success(f"Operation Name: {operation_name}")
                        
                
            branch_elements = root.findall(".//con:branch", namespaces)
            if branch_elements:
                for branch_element in branch_elements:
                    
                    operation_name = branch_element.attrib.get('name', '')
                    
                    st.success(f"Operation Name Branch Elements: {operation_name}")
                    if operation_name in operations:
                        service_element = branch_element.find(".//con1:service", namespaces)
  
                        if service_element is not None:
                            service_ref = service_element.attrib.get('ref', '')
                            services_for_operations[operation_name] = service_ref
                            st.success("branch_elements")
                            st.success(f"Operation Name: {operation_name}, Service Ref: {service_ref}")
                            
                        else:

                            # Si service_element es None, buscar el elemento <con:request> dentro de branch_element
                            request_element = branch_element.find(".//con:request", namespaces)
                            if request_element is not None:
                                request_value = request_element.text
                                print("El valor del elemento <con:request> dentro de branch_element es:", request_value)
                                
                                
                                # Utilizamos XPath para encontrar los elementos 'con:pipeline' con el atributo 'name' igual a 'request_value'
                                pipelines = root.findall(".//con:pipeline[@name='" + request_value + "']", namespaces)

                                # Imprimimos los elementos encontrados (si los hay)
                                for pipeline in pipelines:
                                    print("Se encontró un pipeline con name igual a '{}':".format(request_value))
                                    #print(ET.tostring(pipeline, encoding='unicode'))
                                    
                                    ns_stage_transform_config   = {'con1': 'http://www.bea.com/wli/sb/stages/transform/config'}
                                    ns_stage_publish_config     = {'con1': 'http://www.bea.com/wli/sb/stages/publish/config'}
                                    ns_stage_routing_config     = {'con1': 'http://www.bea.com/wli/sb/stages/routing/config'}
                                    ns_stage_config             = {'con1':'http://www.bea.com/wli/sb/stages/config'}
                                    
                                    ns_stage_pipeline_config    = {'con': 'http://www.bea.com/wli/sb/pipeline/config',
                                                                'con1': 'http://www.bea.com/wli/sb/stages/routing/config',
                                                                'con2': 'http://www.bea.com/wli/sb/stages/config',
                                                                'con3': 'http://www.bea.com/wli/sb/stages/transform/config',
                                                                'ref': 'http://www.bea.com/wli/sb/reference',
                                                                'xsi': 'http://www.w3.org/2001/XMLSchema-instance'}
                                    
                                    ns                           = {'con': 'http://www.example.com',
                                                                    'con4': 'http://www.bea.com/wli/sb/stages/routing/config',
                                                                    'xsi': 'http://www.w3.org/2001/XMLSchema-instance'}
                                    

                                    ws_callouts = pipeline.findall(".//con1:wsCallout", namespaces=ns_stage_transform_config)
                                    #st.success(f"ws_callouts: {ws_callouts}")
                                    java_callouts = pipeline.findall(".//con1:javaCallout", namespaces=ns_stage_transform_config)
                                    #st.success(f"java_callouts: {java_callouts}")
                                    routes = pipeline.findall(".//con1:route", namespaces=ns_stage_publish_config)
                                    #st.success(f"routes: {routes}")
                                    routes2 = pipeline.findall(".//con1:route", namespaces=ns_stage_routing_config)
                                    #st.success(f"routes2: {routes2}")
                                    flow_elements = pipeline.findall(".//con:flow", ns_stage_pipeline_config)
                                    st.success(f"flow_elements: {flow_elements}")
                                    
                                    
                                    for java_callout in java_callouts:
                                        method_element = java_callout.find(".//con1:method", namespaces=ns_stage_transform_config)
                                        if method_element is not None:
                                            method_text = method_element.text
                                            service_element = java_callout.find(".//con1:archive", namespaces=ns_stage_transform_config)
                                            if service_element is not None:
                                                service_ref = service_element.attrib.get('ref', '')
                                                services_for_operations[operation_name] = service_ref
                                                st.success(f"services_for_operations java_callouts: {services_for_operations}")
                                    
                                    for ws_callout in ws_callouts:
                                        service_element = ws_callout.find(".//con1:service", namespaces=ns_stage_transform_config)
                                        operation_element = ws_callout.find(".//con1:operation", namespaces=ns_stage_transform_config)
                                        if service_element is not None and operation_element is not None:
                                            service_ref = service_element.attrib.get('ref', '')
                                            services_for_operations[operation_name] = service_ref
                                            st.success(f"services_for_operations ws_callouts: {services_for_operations}")
                                    
                                    
                                    for route in routes:
                                        service_element = route.find(".//con1:service", namespaces=ns_stage_publish_config)
                                        operation_element = route.find(".//con1:operation", namespaces=ns_stage_publish_config)
                                        if service_element is not None and operation_element is not None:
                                            service_ref = service_element.attrib.get('ref', '')
                                            services_for_operations[operation_name] = service_ref
                                            st.success(f"services_for_operations routes: {services_for_operations}")
                                    
                                    for route in routes2:
                                        service_element = route.find(" .//con1:service", namespaces=ns_stage_routing_config)
                                        operation_element = route.find(" .//con1:operation", namespaces=ns_stage_routing_config)
                                        if service_element is not None and operation_element is not None:
                                            service_ref = service_element.attrib.get('ref', '')
                                            services_for_operations[operation_name] = service_ref
                                            st.success(f"services_for_operations routes2: {services_for_operations}")
                                            
                                     
                                     # Itera sobre cada elemento <con:flow> encontrado
                                    for flow_element in flow_elements:
                                        # Encuentra todos los elementos <con1:service> dentro de <con:flow>
                                        service_elements = flow_element.findall(".//con1:service[@xsi:type='ref:BusinessServiceRef']", ns_stage_pipeline_config)
                                        
                                        # Si no se encuentra ningún servicio dentro del flujo, salta al siguiente flujo
                                        if not service_elements:
                                            continue
                                        
                                        # Itera sobre cada elemento <con1:service> encontrado dentro de <con:flow>
                                        for service_element in service_elements:
                                            # Accede al atributo 'ref' del elemento <con1:service>
                                            service_ref = service_element.attrib.get('ref', '')

                                            # Encuentra todos los elementos <con1:operation> dentro de <con:flow>
                                            operation_elements = flow_element.findall(".//con1:operation", ns_stage_pipeline_config)


                                            operation_element = operation_elements[0]

                                            # Agrega la relación entre el nombre de la operación y la referencia del servicio al diccionario services_for_operations
                                            services_for_operations[operation_name] = service_ref
                                                    

            
            else:                
                route_elements = root.findall(".//con:route-node", namespaces)
                for route_element in route_elements:
                    operation_element = route_element.find(".//con1:operation", namespaces)
                    if operation_element is not None:
                        operation_name = operation_element.text.strip()  
                        if operation_name in operations:
                            service_element = route_element.find(".//con1:service", namespaces)
                            if service_element is not None:
                                service_ref = service_element.attrib.get('ref', '')
                                
                                # Verificar si la operación ya existe en el diccionario
                                new_operation_name = operation_name
                                version = 2
                                while (new_operation_name in services_for_operations and services_for_operations[new_operation_name] != service_ref):
                                    new_operation_name = f"{operation_name}v{version}"
                                    version += 1  # Incrementa la versión si ya existe

                                # Asignar el service_ref con el nuevo nombre de operación
                                services_for_operations[new_operation_name] = service_ref
                                
                                
                                st.success("route_elements")
                                st.success(f"Operation Name: {operation_name}, Service Ref: {service_ref}")
                                
                                 
                # Encuentra todos los elementos <wsCallout> sin importar el prefijo del namespace
                callout_elements = [element for element in root.iter() if element.tag.endswith('wsCallout')]
                
                # Itera sobre cada elemento <wsCallout> encontrado
                for callout_element in callout_elements:
                    operation_name = ""
                    service_ref = ""
                    operation_element = callout_element.find(".//con3:operation", namespaces)
                    if operation_element is not None:
                        operation_name = operation_element.text.strip()
                    service_element = callout_element.find(".//con3:service", namespaces)
                    if service_element is not None:
                        service_ref = service_element.attrib.get('ref', '')
                    if operation_name and service_ref:
                        
                        # Verificar si la operación ya existe en el diccionario
                        new_operation_name = operation_name
                        version = 2
                        while (new_operation_name in services_for_operations and services_for_operations[new_operation_name] != service_ref):
                            new_operation_name = f"{operation_name}v{version}"
                            version += 1  # Incrementa la versión si ya existe

                        # Asignar el service_ref con el nuevo nombre de operación
                        services_for_operations[new_operation_name] = service_ref
                        st.success("callout_element")
                        st.success(f"Operation Name: {operation_name}, Service Ref: {service_ref}")
                        
                        
                
                # Encuentro el nombre de la operación y el servicio con un filtro más específico por 'varName'
                validacion_service_node = True
                validacion_assign_node = True
                service_node = root.findall(".//con4:service", namespaces={"con4": "http://www.bea.com/wli/sb/stages/routing/config"})
                if service_node:
                    service_ref = service_node[0].attrib['ref']
                else:
                    validacion_service_node = False
                    st.success("No se encontró el nodo con la operación")

                # Filtramos por varName="NOMBRE_SERVICIO_TUXEDO" para obtener la expresión correcta
                assign_node = root.findall(".//con1:assign[@varName='NOMBRE_SERVICIO_TUXEDO']", namespaces={"con1": "http://www.bea.com/wli/sb/stages/transform/config"})
                if assign_node:
                    operation_name = assign_node[0].find(".//con2:xqueryText", namespaces={"con2": "http://www.bea.com/wli/sb/stages/config"}).text.strip()
                    operation_name = operation_name.replace(" ", "")
                    operation_name = operation_name.replace("'", "")
                    validacion_assign_node = True
                else:
                    validacion_assign_node = False
                    st.success("No se encontró el nodo assign con varName='NOMBRE_SERVICIO_TUXEDO'")
                    
                    assign_node = root.findall(".//con1:operation", namespaces={"con1": "http://www.bea.com/wli/sb/stages/routing/config"})
                    if assign_node:
                        operation_name = assign_node[0].text.strip()
                        validacion_assign_node = True
               
                # Asigno al diccionario
                if validacion_service_node and not validacion_assign_node:
                    operation_name = service_ref.split("/")[-1]
                    st.success(f"Operation Name: {operation_name}, Service Ref: {service_ref}")
                    
                    # Verificar si la operación ya existe en el diccionario
                    new_operation_name = operation_name
                    version = 2
                    while (new_operation_name in services_for_operations and services_for_operations[new_operation_name] != service_ref):
                        new_operation_name = f"{operation_name}v{version}"
                        version += 1  # Incrementa la versión si ya existe

                    # Asignar el service_ref con el nuevo nombre de operación
                    services_for_operations[new_operation_name] = service_ref
                    
                # Asigno al diccionario
                if validacion_service_node and validacion_assign_node:
                    st.success(f"Operation Name: {operation_name}, Service Ref: {service_ref}")
                    
                    # Verificar si la operación ya existe en el diccionario
                    new_operation_name = operation_name
                    version = 2
                    while (new_operation_name in services_for_operations and services_for_operations[new_operation_name] != service_ref):
                        new_operation_name = f"{operation_name}v{version}"
                        version += 1  # Incrementa la versión si ya existe

                    # Asignar el service_ref con el nuevo nombre de operación
                    services_for_operations[new_operation_name] = service_ref
                                
    st.success(f"SERVICES FOR: {services_for_operations}")
    st.success("***************************** FIN EXTRACT SERVICE OPERATIONS*********************************************")
    
    return services_for_operations

def definir_operaciones_internas_pipeline(pipeline_path):
    service_refs = set()
    services_for_operations = {}
    #st.success("ENTRO A OPERACIONES INTERNAS PIPELINE")
    try:
        with open(pipeline_path, 'r', encoding="utf-8") as f:
            pipeline_content = f.read()
            root = ET.fromstring(pipeline_content)
            
            ns_stage_transform_config   = {'con1': 'http://www.bea.com/wli/sb/stages/transform/config'}
            ns_stage_publish_config     = {'con1': 'http://www.bea.com/wli/sb/stages/publish/config'}
            ns_stage_routing_config     = {'con1': 'http://www.bea.com/wli/sb/stages/routing/config'}
            ns_stage_config             = {'con1':'http://www.bea.com/wli/sb/stages/config'}
            
            ns_stage_pipeline_config    = {'con': 'http://www.bea.com/wli/sb/pipeline/config',
                                        'con1': 'http://www.bea.com/wli/sb/stages/routing/config',
                                        'con2': 'http://www.bea.com/wli/sb/stages/config',
                                        'con3': 'http://www.bea.com/wli/sb/stages/transform/config',
                                        'ref': 'http://www.bea.com/wli/sb/reference',
                                        'xsi': 'http://www.w3.org/2001/XMLSchema-instance'}
            
            ns                           = {'con': 'http://www.example.com',
                                            'con4': 'http://www.bea.com/wli/sb/stages/routing/config',
                                            'xsi': 'http://www.w3.org/2001/XMLSchema-instance'}
            
            ws_callouts = root.findall(".//con1:wsCallout", namespaces=ns_stage_transform_config)
            #st.success(f"ws_callouts: {ws_callouts}")
            
            ws_callouts2 = root.findall(".//con1:wsCallout", namespaces=ns_stage_config)
            
            java_callouts = root.findall(".//con1:javaCallout", namespaces=ns_stage_transform_config)
            #st.success(f"java_callouts: {java_callouts}")
            routes = root.findall(".//con1:route", namespaces=ns_stage_publish_config)
            #st.success(f"routes: {routes}")
            routes2 = root.findall(".//con1:route", namespaces=ns_stage_routing_config)
            #st.success(f"routes2: {routes2}")
            flow_elements = root.findall(".//con:flow", ns_stage_pipeline_config)
            st.success(f"flow_elements: {flow_elements}")
            
            
            for java_callout in java_callouts:
                method_element = java_callout.find(".//con1:method", namespaces=ns_stage_transform_config)
                if method_element is not None:
                    method_text = method_element.text
                    operation_name = method_text.split('(')[0].split()[-1]
                    service_element = java_callout.find(".//con1:archive", namespaces=ns_stage_transform_config)
                    if service_element is not None:
                        service_ref = service_element.attrib.get('ref', '')
                        service_refs.add(service_ref)
                        
                        # Verificar si la operación ya existe en el diccionario
                        new_operation_name = operation_name
                        version = 2
                        while (new_operation_name in services_for_operations and services_for_operations[new_operation_name] != service_ref):
                            new_operation_name = f"{operation_name}v{version}"
                            version += 1  # Incrementa la versión si ya existe

                        # Asignar el service_ref con el nuevo nombre de operación
                        services_for_operations[new_operation_name] = service_ref
                        
                        st.success(f"service_ref: {service_ref} - operation_name: {new_operation_name}")
            
            for ws_callout in ws_callouts:
                service_element = ws_callout.find(".//con1:service", namespaces=ns_stage_transform_config)
                operation_element = ws_callout.find(".//con1:operation", namespaces=ns_stage_transform_config)
                if service_element is not None and operation_element is not None:
                    service_ref = service_element.attrib.get('ref', '')
                    operation_name = operation_element.text
                    service_refs.add(service_ref)
                    
                    # Verificar si la operación ya existe en el diccionario
                    new_operation_name = operation_name
                    version = 2
                    while (new_operation_name in services_for_operations and services_for_operations[new_operation_name] != service_ref):
                        new_operation_name = f"{operation_name}v{version}"
                        version += 1  # Incrementa la versión si ya existe

                    # Asignar el service_ref con el nuevo nombre de operación
                    services_for_operations[new_operation_name] = service_ref
                    
                    st.success(f"service_ref: {service_ref} - operation_name: {new_operation_name}")
            
            for element in root.iter():
                if element.tag.endswith('wsCallout'):
                    service_element = element.find(".//con1:service", namespaces=ns_stage_transform_config)
                    operation_element = element.find(".//con1:operation", namespaces=ns_stage_transform_config)
                    if service_element is not None and operation_element is not None:
                        service_ref = service_element.attrib.get('ref', '')
                        operation_name = operation_element.text
                        service_refs.add(service_ref)
                        
                        # Verificar si la operación ya existe en el diccionario
                        new_operation_name = operation_name
                        version = 2
                        while (new_operation_name in services_for_operations and services_for_operations[new_operation_name] != service_ref):
                            new_operation_name = f"{operation_name}v{version}"
                            version += 1  # Incrementa la versión si ya existe

                        # Asignar el service_ref con el nuevo nombre de operación
                        services_for_operations[new_operation_name] = service_ref
                        
                        st.success(f"service_ref: {service_ref} - operation_name: {new_operation_name}")
                      
                        
            #2 Forma de encontrar ws_callouts:
            
            for ws_callout in ws_callouts2:
                service_element = ws_callout.find(".//con1:service", namespaces=ns_stage_config)
                operation_element = ws_callout.find(".//con1:operation", namespaces=ns_stage_config)
                if service_element is not None and operation_element is not None:
                    service_ref = service_element.attrib.get('ref', '')
                    operation_name = operation_element.text
                    service_refs.add(service_ref)
                    
                    # Verificar si la operación ya existe en el diccionario
                    new_operation_name = operation_name
                    version = 2
                    while (new_operation_name in services_for_operations and services_for_operations[new_operation_name] != service_ref):
                        new_operation_name = f"{operation_name}v{version}"
                        version += 1  # Incrementa la versión si ya existe

                    # Asignar el service_ref con el nuevo nombre de operación
                    services_for_operations[new_operation_name] = service_ref
                    
                    st.success(f"service_ref: {service_ref} - operation_name: {new_operation_name}")
            
            for element in root.iter():
                if element.tag.endswith('wsCallout'):
                    service_element = element.find(".//con1:service", namespaces=ns_stage_config)
                    operation_element = element.find(".//con1:operation", namespaces=ns_stage_config)
                    if service_element is not None and operation_element is not None:
                        service_ref = service_element.attrib.get('ref', '')
                        operation_name = operation_element.text
                        service_refs.add(service_ref)
                        
                        # Verificar si la operación ya existe en el diccionario
                        new_operation_name = operation_name
                        version = 2
                        while (new_operation_name in services_for_operations and services_for_operations[new_operation_name] != service_ref):
                            new_operation_name = f"{operation_name}v{version}"
                            version += 1  # Incrementa la versión si ya existe

                        # Asignar el service_ref con el nuevo nombre de operación
                        services_for_operations[new_operation_name] = service_ref
                        
                        st.success(f"service_ref: {service_ref} - operation_name: {new_operation_name}")
                        
            for route in routes:
                service_element = route.find(".//con1:service", namespaces=ns_stage_publish_config)
                operation_element = route.find(".//con1:operation", namespaces=ns_stage_publish_config)
                if service_element is not None and operation_element is not None:
                    service_ref = service_element.attrib.get('ref', '')
                    operation_name = operation_element.text
                    service_refs.add(service_ref)
                    
                    # Verificar si la operación ya existe en el diccionario
                    new_operation_name = operation_name
                    version = 2
                    while (new_operation_name in services_for_operations and services_for_operations[new_operation_name] != service_ref):
                        new_operation_name = f"{operation_name}v{version}"
                        version += 1  # Incrementa la versión si ya existe

                    # Asignar el service_ref con el nuevo nombre de operación
                    services_for_operations[new_operation_name] = service_ref
                    
                    st.success(f"service_ref: {service_ref} - operation_name: {new_operation_name}")
            
            #2 Forma de encontrar routes2:
            
            ns_con2 = {'con2': 'http://www.bea.com/wli/sb/stages/routing/config'}

            # Encuentra todos los elementos 'con2:route' dentro de 'con:flow'
            route_elements = root.findall(".//con2:route", namespaces=ns_con2)
            st.success(f"route_elements final : {route_elements}")

            # Itera sobre cada elemento 'con2:route' encontrado
            for route in route_elements:
                # Encuentra el elemento 'con2:service' dentro de 'con2:route'
                service_element = route.find(".//con2:service", namespaces=ns_con2)
                
                st.success(f"route_elements final : {service_element}")
                
                # Encuentra el elemento 'con2:operation' dentro de 'con2:route'
                operation_element = route.find(".//con2:operation", namespaces=ns_con2)
                
                # Verifica si ambos elementos 'con2:service' y 'con2:operation' existen
                if service_element is not None and operation_element is not None:
                    # Obtén el valor del atributo 'ref' de 'con2:service'
                    service_ref = service_element.attrib.get('ref', '')
                    
                    # Obtén el texto dentro de 'con2:operation'
                    operation_name = operation_element.text
                    
                    # Agrega el servicio y la operación al diccionario 'services_for_operations'
                    service_refs.add(service_ref)
                    
                    # Verificar si la operación ya existe en el diccionario
                    new_operation_name = operation_name
                    version = 2
                    while (new_operation_name in services_for_operations and services_for_operations[new_operation_name] != service_ref):
                        new_operation_name = f"{operation_name}v{version}"
                        version += 1  # Incrementa la versión si ya existe

                    # Asignar el service_ref con el nuevo nombre de operación
                    services_for_operations[new_operation_name] = service_ref
                    
                    st.success(f"service_ref: {service_ref} - operation_name: {new_operation_name}")
                            
             
             # Itera sobre cada elemento <con:flow> encontrado
            for flow_element in flow_elements:
                # Encuentra todos los elementos <con1:service> dentro de <con:flow>
                service_elements = flow_element.findall(".//con1:service[@xsi:type='ref:BusinessServiceRef']", ns_stage_pipeline_config)
                
                # Si no se encuentra ningún servicio dentro del flujo, salta al siguiente flujo
                if not service_elements:
                    continue
                
                # Itera sobre cada elemento <con1:service> encontrado dentro de <con:flow>
                for service_element in service_elements:
                    # Accede al atributo 'ref' del elemento <con1:service>
                    service_ref = service_element.attrib.get('ref', '')

                    # Encuentra todos los elementos <con1:operation> dentro de <con:flow>
                    operation_elements = flow_element.findall(".//con1:operation", ns_stage_pipeline_config)

                    # Si no se encuentra ningún elemento <con1:operation>, establece un valor predeterminado
                    if not operation_elements:
                        operation_name = service_ref.split('/')[-1]
                    else:
                        # Obtiene el texto del primer elemento <con1:operation>, que es el nombre de la operación
                        operation_element = operation_elements[0]
                        operation_name = operation_element.text.strip()

                    # Verificar si la operación ya existe en el diccionario
                    new_operation_name = operation_name
                    version = 2
                    while (new_operation_name in services_for_operations and services_for_operations[new_operation_name] != service_ref):
                        new_operation_name = f"{operation_name}v{version}"
                        version += 1  # Incrementa la versión si ya existe

                    # Asignar el service_ref con el nuevo nombre de operación
                    services_for_operations[new_operation_name] = service_ref
                    
                    st.success(f"service_ref: {service_ref} - operation_name: {new_operation_name}")
            
            st.success(f"service_refs: {service_refs}")
            st.success(f"Flow Elements Services: {services_for_operations}")

                   

        return services_for_operations
    except FileNotFoundError:
        print(f"El archivo {pipeline_path} no pudo ser encontrado.")

def extract_osb_services_with_given_path_dict(jdeveloper_projects_dir, services_for_operations):
    osb_services = []
    for service_dict in services_for_operations:
        for service_path, path2 in service_dict.items():
            #
            #st.success("*****************************INICIO EXTRACT_OSB_SERVICES_WITH_GIVEN_PATH DICT*********************************************")
            #
            #st.success(f"path2: {path2}")
            proxy_name = path2.split('/')[-1]
            if 'Proxies' in path2:    
                osb_file_path = os.path.join(jdeveloper_projects_dir, path2 + ".ProxyService")
                #st.success(f"osb_file_path: {osb_file_path}")
                #
                project_name = extract_project_name_from_proxy(osb_file_path)
                #st.success(f"project_name: {project_name}")
                #
                if project_name is None:
                    osb_services.append((service_path, proxy_name, 'N/A'))
                    continue  # Salta este registro y continúa con el siguiente
                pipeline_path = extract_pipeline_path_from_proxy(osb_file_path, jdeveloper_projects_dir)
                #st.success(f"pipeline_path: {pipeline_path}")
                #
                with open(osb_file_path, 'r', encoding="utf-8") as f:
                    content = f.read()
                    service_name = os.path.splitext(os.path.basename(osb_file_path))[0]
                    wsdl_relative_path = extract_wsdl_relative_path(content)
                    #st.success("*****************************INICIO EXTRACT_OSB_SERVICES_WITH_GIVEN_PATH DICT*********************************************")
                    #
                    #st.success(f"service_name: {service_name}")
                    #st.success(f"wsdl_relative_path: {wsdl_relative_path}")
                    #
                    if wsdl_relative_path:
                        wsdl_path = os.path.join(jdeveloper_projects_dir, wsdl_relative_path + ".WSDL")
                        #st.success("*****************************INICIO EXTRACT_OSB_SERVICES_WITH_GIVEN_PATH DICT*********************************************")
                        #
                        #st.success(f"wsdl_path: {wsdl_path}")
                        #st.success("*****************************INICIO EXTRACT_OSB_SERVICES_WITH_GIVEN_PATH DICT*********************************************")
                        #
                        operations = extract_wsdl_operations(wsdl_path)
                        #st.success(f"operations: {operations}")
                        #
                        #st.success("*****************************INICIO EXTRACT_OSB_SERVICES_WITH_GIVEN_PATH DICT*********************************************")
                        #
                        #Se comenta linea para revisar como se hace:
                        #service_for_operations = extract_service_for_operations(pipeline_path, operations)
                        
                        service_for_operations = ""
                        #st.success(f"service_for_operations: {service_for_operations}")
                        #
                        if not service_for_operations:
                            service_refs = extract_service_refs_from_pipeline(pipeline_path)
                            #st.success("*****************************INICIO EXTRACT_OSB_SERVICES_WITH_GIVEN_PATH DICT*********************************************")
                            #
                            #st.success(f"service_refs: {service_refs}")
                            #
                            for service_ref in service_refs:
                                osb_services.append((service_path, proxy_name, service_ref))
                            if not service_refs:
                                osb_services.append((service_path, proxy_name, 'N/A'))
                        else:
                            #st.success("*****************************INICIO EXTRACT_OSB_SERVICES_WITH_GIVEN_PATH DICT*********************************************")
                            #
                            business_service = list(service_for_operations.values())[0]
                            osb_services.append((service_path, proxy_name, business_service))
                            #st.success(f"osb_services: {osb_services}")
                            #
            
            #elif 'BusinessServices' in path2:
                            
            
            else:
                osb_services.append((service_path, proxy_name, 'N/A'))
                continue
    #st.success("*****************************FIN EXTRACT_OSB_SERVICES_WITH_GIVEN_PATH DICT*********************************************")
    #
    return osb_services

def extract_osb_services_references_abc2(jdeveloper_projects_dir, services_for_operations):
    osb_services = []
    es_ebs = False
    service_ref = ""
    
    st.success("Entro a extract_osb_services_references_abc2")
    
    st.success(f"jdeveloper_projects_dir : {jdeveloper_projects_dir}")
    
    
    if services_for_operations is not None:
        for operacion, proxy_ebs1, referencia, operacion_legado in services_for_operations:
            st.success(f"operacion: {operacion}")
            st.success(f"proxy_ebs1: {proxy_ebs1}")
            proxy_ebs2 = proxy_ebs1
            proxy_ebs3 = proxy_ebs1
            st.success(f"referencia: {referencia}")
            st.success(f"operacion_legado: {operacion_legado}")
            
            palabras_invalidas = ['ComponentesComunes/Proxies/PS_ManejadorGenericoErroresV1.0', 'N/A', 'Resources/Jars']
            if referencia not in palabras_invalidas:
                if 'EBS' in referencia: #Saber si es un EBS
                    es_ebs = True
                    st.success("Es EBS")
                    
                    if 'Proxies' in referencia:
                        st.success(f"Proxies esta en referencia : {referencia}")
                        
                        osb_file_path = os.path.join(jdeveloper_projects_dir, referencia + ".ProxyService")
                        st.success(f"osb_file_path : {osb_file_path}")
                        
                        project_name = extract_project_name_from_proxy(osb_file_path)
                        if project_name is None:
                            osb_services.append((operacion , proxy_ebs1, proxy_ebs2, proxy_ebs3, referencia, operacion_legado, 'N/A', 'N/A'))
                            st.success(f"project_name es 'None' : {project_name}")
                            
                            
                            st.success(f"osb_services: {osb_services}")
                            
                            continue

                        pipeline_path = extract_pipeline_path_from_proxy(osb_file_path, jdeveloper_projects_dir)
                        st.success(f"pipeline_path: {pipeline_path}")
                        
                        with open(osb_file_path, 'r', encoding="utf-8") as f:
                            content = f.read()
                            service_name = os.path.splitext(os.path.basename(osb_file_path))[0]
                            wsdl_relative_path = extract_wsdl_relative_path(content)

                            if wsdl_relative_path:
                                wsdl_path = os.path.join(jdeveloper_projects_dir, wsdl_relative_path + ".WSDL")
                                st.success(f"wsdl_path: {wsdl_path}")
                                
                                operations = extract_wsdl_operations(wsdl_path)
                                st.success(f"operations: {operations}")
                                
                                service_for_operations = extract_service_for_operations(pipeline_path, operacion_legado)
                                st.success(f"service_for_operations: {service_for_operations}")
                                

                                if not service_for_operations:
                                    service_refs = extract_service_refs_from_pipeline(pipeline_path)
                                    st.success(f"service_for_operations 2: {service_for_operations}")
                                    

                                    for service_ref in service_refs:
                                        osb_services.append((operacion , proxy_ebs1, proxy_ebs2, proxy_ebs3, referencia, operacion_legado, service_ref, operacion_legado))
                                        st.success(f"operacion {operacion}")
                                        st.success(f"proxy_ebs1 {proxy_ebs1}")
                                        st.success(f"referencia {referencia}")
                                        st.success(f"operacion_legado {operacion_legado}")
                                        st.success(f"service_ref {service_ref}")
                                        st.success(f"operacion_legado {operacion_legado}")
                                        
                                        
                                        st.success(f"osb_services: {osb_services}")
                                        

                                else:
                                    for operation, proxy_interno in service_for_operations.items():
                                        st.success(f"operacion {operacion}")
                                        st.success(f"proxy_ebs1 {proxy_ebs1}")
                                        st.success(f"referencia {referencia}")
                                        st.success(f"operacion_legado {operacion_legado}")
                                        st.success(f"proxy_interno {proxy_interno}")
                                        
                                        if 'EBS' in referencia and 'PS' in proxy_interno:
                                            proxy_ebs2 = referencia.split("/")[-1]
                                            proxy_ebs3 = proxy_interno.split("/")[-1]
                                        elif 'EBS' in proxy_interno:
                                            proxy_ebs3 = proxy_interno.split("/")[-1]
                                        else:
                                            proxy_ebs3 = proxy_interno
                                        
                                        es_business_service = '/BusinessServices'
                                        if es_business_service not in proxy_interno:
                                            osb_file_path = os.path.join(jdeveloper_projects_dir, proxy_interno + ".ProxyService")
                                            
                                            st.success(f"osb_file_path {osb_file_path}")
                                            
                                            ruta_pipeline = extract_pipeline_path_from_proxy(osb_file_path, jdeveloper_projects_dir)
                                            st.success(f"ruta_pipeline: {ruta_pipeline}")
                                            if ruta_pipeline is None:
                                                osb_services.append((operacion , proxy_ebs1, proxy_ebs2, proxy_ebs3, referencia, operacion_legado, 'N/A', 'N/A'))
                                                st.success(f"ruta_pipeline es 'None' : {project_name}")
                                                st.success(f"operacion {operacion}")
                                                st.success(f"proxy_ebs1 {proxy_ebs1}")
                                                st.success(f"referencia {referencia}")
                                                st.success(f"operacion_legado {operacion_legado}")
                                                st.success(f"service_ref {service_ref}")
                                                st.success(f"operacion_legado {operacion_legado}")
                                                
                                                
                                                st.success(f"osb_services: {osb_services}")
                                                
                                                continue
                                            operaciones_internas = definir_operaciones_internas_pipeline(ruta_pipeline)
                                            
                                            st.success(f"operaciones_internas {operaciones_internas}")
                                            proxy_ebs3_momento = proxy_ebs3
                                            st.success(f"proxy_ebs3_momento {proxy_ebs3_momento}")
                                            
                                            for clave, valor in operaciones_internas.items():
                                                operacion_legado = clave
                                                proxy_interno = valor.split("/")[-1]
                                                st.success(f"clave {clave}")
                                                
                                                st.success(f"valor {valor}")
                                                proxy_ebs3 = proxy_ebs3_momento
                                                st.success(f"proxy_ebs3 {proxy_ebs3}")
                                                
                                                if es_business_service in valor:
                                                    
                                                    proxy_abc_ebs = proxy_ebs2+"/"+proxy_ebs3
                                                    osb_file_path = os.path.join(jdeveloper_projects_dir, valor + ".BusinessService")
                                                    project_name = extract_project_name_from_business(osb_file_path)
                                                    st.success(f"project_name es : {project_name}")
                                                    if project_name is None:
                                                        st.success(f"project_name es 'None' : {project_name}")
                                                        
                                                        continue

                                                    with open(osb_file_path, 'r', encoding="utf-8") as f:
                                                        content = f.read()
                                                        service_name = os.path.splitext(os.path.basename(osb_file_path))[0]
                                                        st.success(f"service_name: {service_name}")
                                                        wsdl_relative_path = extract_wsdl_relative_path(content)

                                                        wsdl_path = os.path.join(jdeveloper_projects_dir, wsdl_relative_path + ".WSDL")
                                                        operations = extract_wsdl_operations(wsdl_path)
                                                        service_refs = extract_uri_and_provider_id_from_bix(osb_file_path)
                                                        st.success(f"service_refs: {service_refs}")
                                                        

                                                        for uri_value, provider_id_value in service_refs:
                                                            
                                                            st.success(f"DATOS {operacion , proxy_ebs1, proxy_ebs2, proxy_abc_ebs, valor, operacion_legado, uri_value, provider_id_value}")
                                                            osb_services.append((operacion , proxy_ebs1, proxy_ebs2, proxy_abc_ebs, valor, operacion_legado, uri_value, provider_id_value))
                                                
                                                else:
                                                
                                                    if 'EBS' in valor:
                                                        valor_limpio = valor.split("/")[-1]
                                                        st.success(f"valor_limpio: {valor_limpio}")
                                                        proxy_ebs3 = proxy_ebs3_momento+"/"+valor_limpio
                                                        st.success(f"proxy_ebs2: {proxy_ebs2}")
                                                        st.success(f"proxy_ebs3: {proxy_ebs3}")
                                                        proxy_anterior = proxy_ebs3
                                                        
                                                        if 'Proxies' in valor:
                                                            st.success(f"Proxies esta en valor : {valor}")
                                                            
                                                            osb_file_path = os.path.join(jdeveloper_projects_dir, valor + ".ProxyService")
                                                            st.success(f"osb_file_path : {osb_file_path}")
                                                            
                                                            project_name = extract_project_name_from_proxy(osb_file_path)
                                                            if project_name is None:
                                                                osb_services.append((operacion , proxy_ebs1, proxy_ebs2, proxy_ebs3, valor, operacion_legado, 'N/A', 'N/A'))
                                                                st.success(f"project_name es 'None' : {project_name}")
                                                                
                                                                
                                                                st.success(f"osb_services: {osb_services}")
                                                                
                                                                continue

                                                            pipeline_path = extract_pipeline_path_from_proxy(osb_file_path, jdeveloper_projects_dir)
                                                            st.success(f"pipeline_path: {pipeline_path}")
                                                            
                                                            with open(osb_file_path, 'r', encoding="utf-8") as f:
                                                                content = f.read()
                                                                service_name = os.path.splitext(os.path.basename(osb_file_path))[0]
                                                                wsdl_relative_path = extract_wsdl_relative_path(content)

                                                                if wsdl_relative_path:
                                                                    wsdl_path = os.path.join(jdeveloper_projects_dir, wsdl_relative_path + ".WSDL")
                                                                    st.success(f"wsdl_path: {wsdl_path}")
                                                                    
                                                                    operations = extract_wsdl_operations(wsdl_path)
                                                                    st.success(f"operations: {operations}")
                                                                    
                                                                    service_for_operations = extract_service_for_operations(pipeline_path, operacion_legado)
                                                                    st.success(f"service_for_operations: {service_for_operations}")
                                                                    
                                                                    proxy_ebs3_momento = proxy_ebs3

                                                                    if not service_for_operations:
                                                                        service_refs = extract_service_refs_from_pipeline(pipeline_path)
                                                                        st.success(f"service_for_operations 2: {service_for_operations}")
                                                                        

                                                                        for service_ref in service_refs:
                                                                            osb_services.append((operacion , proxy_ebs1, proxy_ebs2, proxy_ebs3, referencia, operacion_legado, service_ref, operacion_legado))
                                                                            st.success(f"operacion {operacion}")
                                                                            st.success(f"proxy_ebs1 {proxy_ebs1}")
                                                                            st.success(f"referencia {referencia}")
                                                                            st.success(f"operacion_legado {operacion_legado}")
                                                                            st.success(f"service_ref {service_ref}")
                                                                            st.success(f"operacion_legado {operacion_legado}")
                                                                            
                                                                            
                                                                            st.success(f"osb_services: {osb_services}")
                                                                            

                                                                    else:
                                                                        for operation, proxy_interno in service_for_operations.items():
                                                                            st.success(f"operacion {operacion}")
                                                                            st.success(f"proxy_ebs1 {proxy_ebs1}")
                                                                            st.success(f"referencia {referencia}")
                                                                            st.success(f"proxy_ebs3_momento {proxy_ebs3_momento}")
                                                                            st.success(f"operacion_legado {operacion_legado}")
                                                                            st.success(f"proxy_interno {proxy_interno}")
                                                                            
                                                                            if 'EBS' in referencia and 'PS' in proxy_ebs3_momento:
                                                                                proxy_ebs2 = referencia.split("/")[-1]
                                                                                proxy_ebs3 = proxy_interno.split("/")[-1]
                                                                                st.success(f"proxy_ebs2: {proxy_ebs2}")
                                                                                st.success(f"proxy_ebs3: {proxy_ebs3}")
                                                                            
                                                                            es_business_service = '/BusinessServices'
                                                                            proxy_concatenado = proxy_interno.split("/")[-1]
                                                                            st.success(f"proxy_concatenado {proxy_concatenado}")
                                                                            proxy_ebs3 = proxy_ebs3_momento+"/"+proxy_concatenado
                                                                            st.success(f"proxy_ebs3 {proxy_ebs3}")
                                                                            if es_business_service not in proxy_interno:
                                                                                osb_file_path = os.path.join(jdeveloper_projects_dir, proxy_interno + ".ProxyService")
                                                                                
                                                                                st.success(f"osb_file_path {osb_file_path}")
                                                                                
                                                                                ruta_pipeline = extract_pipeline_path_from_proxy(osb_file_path, jdeveloper_projects_dir)
                                                                                st.success(f"ruta_pipeline: {ruta_pipeline}")
                                                                                if ruta_pipeline is None:
                                                                                    osb_services.append((operacion , proxy_ebs1, proxy_ebs2, proxy_ebs3, referencia, operacion_legado, 'N/A', 'N/A'))
                                                                                    st.success(f"ruta_pipeline es 'None' : {project_name}")
                                                                                    st.success(f"operacion {operacion}")
                                                                                    st.success(f"proxy_ebs1 {proxy_ebs1}")
                                                                                    st.success(f"referencia {referencia}")
                                                                                    st.success(f"operacion_legado {operacion_legado}")
                                                                                    st.success(f"service_ref {service_ref}")
                                                                                    st.success(f"operacion_legado {operacion_legado}")
                                                                                    
                                                                                    
                                                                                    st.success(f"osb_services: {osb_services}")
                                                                                    
                                                                                    continue
                                                                                operaciones_internas = definir_operaciones_internas_pipeline(ruta_pipeline)
                                                                                
                                                                                st.success(f"operaciones_internas {operaciones_internas}")
                                                                                
                                                                                for clave, valor in operaciones_internas.items():
                                                                                    operacion_legado = clave
                                                                                    proxy_externo = valor.split("/")[-1]
                                                                                    st.success(f"clave {clave}")
                                                                                    
                                                                                    st.success(f"valor {valor}")
                                                                                    
                                                                                    if es_business_service in valor:
                                                                                        
                                                                                        osb_file_path = os.path.join(jdeveloper_projects_dir, valor + ".BusinessService")
                                                                                        project_name = extract_project_name_from_business(osb_file_path)
                                                                                        st.success(f"project_name es : {project_name}")
                                                                                        if project_name is None:
                                                                                            st.success(f"project_name es 'None' : {project_name}")
                                                                                            
                                                                                            continue

                                                                                        with open(osb_file_path, 'r', encoding="utf-8") as f:
                                                                                            content = f.read()
                                                                                            service_name = os.path.splitext(os.path.basename(osb_file_path))[0]
                                                                                            st.success(f"service_name: {service_name}")
                                                                                            wsdl_relative_path = extract_wsdl_relative_path(content)

                                                                                            wsdl_path = os.path.join(jdeveloper_projects_dir, wsdl_relative_path + ".WSDL")
                                                                                            operations = extract_wsdl_operations(wsdl_path)
                                                                                            service_refs = extract_uri_and_provider_id_from_bix(osb_file_path)
                                                                                            st.success(f"service_refs: {service_refs}")
                                                                                            

                                                                                            for uri_value, provider_id_value in service_refs:
                                                                                                st.success(f"DATOS {operacion , proxy_ebs1, proxy_ebs2, proxy_ebs3, valor, operacion_legado, uri_value, provider_id_value}")
                                                                                                osb_services.append((operacion , proxy_ebs1, proxy_ebs2, proxy_ebs3, valor, operacion_legado, uri_value, provider_id_value))
                                                                                    
                                                                                    else:
                                                                                    
                                                                                        if 'EBS' in valor:
                                                                                            valor_limpio = valor.split("/")[-1]
                                                                                            proxy_ebs3 = proxy_ebs3+"/"+valor_limpio
                                                                                            
                                                                                            
                                                                                    
                                                                                        
                                                                                        
                                                                                        
                                                                                        else:
                                                                                            st.success(f"proxy_ebs2: {proxy_ebs2}")
                                                                                            st.success(f"proxy_ebs3: {proxy_ebs3}")
                                                                                            st.success(f"DATOS {operacion , proxy_ebs1, proxy_ebs2, proxy_ebs3, valor, operacion_legado, proxy_externo, clave}")
                                                                                            osb_services.append((operacion , proxy_ebs1, proxy_ebs2, proxy_ebs3, valor, operacion_legado, proxy_externo, clave))
                                                                                            st.success(f"operacion {operacion}")
                                                                                            st.success(f"proxy_ebs1 {proxy_ebs1}")
                                                                                            st.success(f"referencia {referencia}")
                                                                                            st.success(f"operacion_legado {operacion_legado}")
                                                                                            st.success(f"operacion_legado {operacion_legado}")
                                                                                            
                                                                                            
                                                                                            st.success(f"osb_services: {osb_services}")
                                                                                            
                                                                            
                                                                            else:
                                                                                osb_file_path = os.path.join(jdeveloper_projects_dir, proxy_interno + ".BusinessService")
                                                                                project_name = extract_project_name_from_business(osb_file_path)
                                                                                st.success(f"project_name es : {project_name}")
                                                                                if project_name is None:
                                                                                    st.success(f"project_name es 'None' : {project_name}")
                                                                                    
                                                                                    continue

                                                                                with open(osb_file_path, 'r', encoding="utf-8") as f:
                                                                                    content = f.read()
                                                                                    service_name = os.path.splitext(os.path.basename(osb_file_path))[0]
                                                                                    st.success(f"service_name: {service_name}")
                                                                                    wsdl_relative_path = extract_wsdl_relative_path(content)

                                                                                    wsdl_path = os.path.join(jdeveloper_projects_dir, wsdl_relative_path + ".WSDL")
                                                                                    operations = extract_wsdl_operations(wsdl_path)
                                                                                    service_refs = extract_uri_and_provider_id_from_bix(osb_file_path)
                                                                                    st.success(f"service_refs: {service_refs}")
                                                                                    

                                                                                    for uri_value, provider_id_value in service_refs:
                                                                                        osb_services.append((operacion , proxy_ebs1, proxy_ebs2, proxy_ebs3, referencia, operacion_legado, uri_value, provider_id_value))
                                                                                        st.success(f"operacion {operacion}")
                                                                                        st.success(f"proxy_ebs1 {proxy_ebs1}")
                                                                                        st.success(f"referencia {referencia}")
                                                                                        st.success(f"operacion_legado {operacion_legado}")
                                                                                        st.success(f"uri_value {uri_value}")
                                                                                        st.success(f"provider_id_value {provider_id_value}")
                                                                                        
                                                                                        st.success(f"osb_services: {osb_services}")
                                                                                        
                                                                                
                                                                            
                                                                            st.success(f"osb_services: {osb_services}")
                                                                            
                                                                            proxy_ebs3 = ""
                                                                            

                                                    else:
                                                        
                                                        if 'Proxies' in valor:
                                                            valor_limpio = valor.split("/")[-1]
                                                            st.success(f"valor_limpio: {valor_limpio}")
                                                            proxy_ebs3 = proxy_ebs3_momento+"/"+valor_limpio
                                                            st.success(f"proxy_ebs3: {proxy_ebs3}")
                                                            st.success(f"Proxies esta en valor : {valor}")
                                                            
                                                            osb_file_path = os.path.join(jdeveloper_projects_dir, valor + ".ProxyService")
                                                            st.success(f"osb_file_path : {osb_file_path}")
                                                            
                                                            project_name = extract_project_name_from_proxy(osb_file_path)
                                                            if project_name is None:
                                                                osb_services.append((operacion , proxy_ebs1, proxy_ebs2, proxy_ebs3, valor, operacion_legado, 'N/A', 'N/A'))
                                                                st.success(f"project_name es 'None' : {project_name}")
                                                                
                                                                
                                                                st.success(f"osb_services: {osb_services}")
                                                                
                                                                continue

                                                            pipeline_path = extract_pipeline_path_from_proxy(osb_file_path, jdeveloper_projects_dir)
                                                            st.success(f"pipeline_path: {pipeline_path}")
                                                            
                                                            with open(osb_file_path, 'r', encoding="utf-8") as f:
                                                                content = f.read()
                                                                service_name = os.path.splitext(os.path.basename(osb_file_path))[0]
                                                                wsdl_relative_path = extract_wsdl_relative_path(content)

                                                                if wsdl_relative_path:
                                                                    wsdl_path = os.path.join(jdeveloper_projects_dir, wsdl_relative_path + ".WSDL")
                                                                    st.success(f"wsdl_path: {wsdl_path}")
                                                                    
                                                                    operations = extract_wsdl_operations(wsdl_path)
                                                                    st.success(f"operations: {operations}")
                                                                    
                                                                    service_for_operations = extract_service_for_operations(pipeline_path, operacion_legado)
                                                                    st.success(f"service_for_operations: {service_for_operations}")
                                                                    

                                                                    if not service_for_operations:
                                                                        service_refs = extract_service_refs_from_pipeline(pipeline_path)
                                                                        st.success(f"service_for_operations 2: {service_for_operations}")
                                                                        

                                                                        for service_ref in service_refs:
                                                                            osb_services.append((operacion , proxy_ebs1, proxy_ebs2, proxy_ebs3, valor, operacion_legado, service_ref, operacion_legado))
                                                                            st.success(f"operacion {operacion}")
                                                                            st.success(f"proxy_ebs1 {proxy_ebs1}")
                                                                            st.success(f"valor {valor}")
                                                                            st.success(f"operacion_legado {operacion_legado}")
                                                                            st.success(f"service_ref {service_ref}")
                                                                            st.success(f"operacion_legado {operacion_legado}")
                                                                            
                                                                            
                                                                            st.success(f"osb_services: {osb_services}")
                                                                            

                                                                    else:
                                                                        for operation, proxy_interno in service_for_operations.items():
                                                                            st.success(f"operacion {operacion}")
                                                                            st.success(f"proxy_ebs1 {proxy_ebs1}")
                                                                            st.success(f"valor {valor}")
                                                                            st.success(f"operacion_legado {operacion_legado}")
                                                                            st.success(f"proxy_interno {proxy_interno}")
                                                                            
                                                                            if 'EBS' in valor and 'PS' in proxy_interno:
                                                                                proxy_ebs2 = valor.split("/")[-1]
                                                                                proxy_ebs3 = proxy_interno.split("/")[-1]
                                                                            elif 'EBS' in proxy_interno:
                                                                                proxy_ebs3 = proxy_interno.split("/")[-1]
                                                                            else:
                                                                                proxy_ebs3 = proxy_interno
                                                                            
                                                                            es_business_service = '/BusinessServices'
                                                                            if es_business_service not in proxy_interno:
                                                                                osb_file_path = os.path.join(jdeveloper_projects_dir, proxy_interno + ".ProxyService")
                                                                                
                                                                                st.success(f"osb_file_path {osb_file_path}")
                                                                                
                                                                                ruta_pipeline = extract_pipeline_path_from_proxy(osb_file_path, jdeveloper_projects_dir)
                                                                                st.success(f"ruta_pipeline: {ruta_pipeline}")
                                                                                if ruta_pipeline is None:
                                                                                    osb_services.append((operacion , proxy_ebs1, proxy_ebs2, proxy_ebs3, valor, operacion_legado, 'N/A', 'N/A'))
                                                                                    st.success(f"ruta_pipeline es 'None' : {project_name}")
                                                                                    st.success(f"operacion {operacion}")
                                                                                    st.success(f"proxy_ebs1 {proxy_ebs1}")
                                                                                    st.success(f"valor {valor}")
                                                                                    st.success(f"operacion_legado {operacion_legado}")
                                                                                    st.success(f"service_ref {service_ref}")
                                                                                    st.success(f"operacion_legado {operacion_legado}")
                                                                                    
                                                                                    
                                                                                    st.success(f"osb_services: {osb_services}")
                                                                                    
                                                                                    continue
                                                                                operaciones_internas = definir_operaciones_internas_pipeline(ruta_pipeline)
                                                                                
                                                                                st.success(f"operaciones_internas {operaciones_internas}")
                                                                                proxy_ebs3_momento = proxy_ebs3
                                                                                st.success(f"proxy_ebs3_momento {proxy_ebs3_momento}")
                                                                                
                                                                                for clave, valor in operaciones_internas.items():
                                                                                    operacion_legado = clave
                                                                                    proxy_interno = valor.split("/")[-1]
                                                                                    st.success(f"clave {clave}")
                                                                                    
                                                                                    st.success(f"valor {valor}")
                                                                                    
                                                                                    if es_business_service in valor:
                                                                                        
                                                                                        osb_file_path = os.path.join(jdeveloper_projects_dir, valor + ".BusinessService")
                                                                                        project_name = extract_project_name_from_business(osb_file_path)
                                                                                        st.success(f"project_name es : {project_name}")
                                                                                        if project_name is None:
                                                                                            st.success(f"project_name es 'None' : {project_name}")
                                                                                            
                                                                                            continue

                                                                                        with open(osb_file_path, 'r', encoding="utf-8") as f:
                                                                                            content = f.read()
                                                                                            service_name = os.path.splitext(os.path.basename(osb_file_path))[0]
                                                                                            st.success(f"service_name: {service_name}")
                                                                                            wsdl_relative_path = extract_wsdl_relative_path(content)

                                                                                            wsdl_path = os.path.join(jdeveloper_projects_dir, wsdl_relative_path + ".WSDL")
                                                                                            operations = extract_wsdl_operations(wsdl_path)
                                                                                            service_refs = extract_uri_and_provider_id_from_bix(osb_file_path)
                                                                                            st.success(f"service_refs: {service_refs}")
                                                                                            

                                                                                            for uri_value, provider_id_value in service_refs:
                                                                                                
                                                                                                st.success(f"DATOS {operacion , proxy_ebs1, proxy_ebs2, proxy_ebs3, valor, operacion_legado, uri_value, provider_id_value}")
                                                                                                osb_services.append((operacion , proxy_ebs1, proxy_ebs2, proxy_ebs3, valor, operacion_legado, uri_value, provider_id_value))
                                                                                
                                                    
                                                    
                                                        else:
                                                            valor_limpio = valor.split("/")[-1]
                                                            st.success(f"valor_limpio: {valor_limpio}")
                                                            proxy_ebs3 = proxy_ebs3_momento+"/"+valor_limpio
                                                            st.success(f"DATOS {operacion , proxy_ebs1, proxy_ebs2, proxy_ebs3, valor, operacion_legado, proxy_interno, clave}")
                                                            osb_services.append((operacion , proxy_ebs1, proxy_ebs2, proxy_ebs3, valor, operacion_legado, proxy_interno, clave))
                                                            st.success(f"operacion {operacion}")
                                                            st.success(f"proxy_ebs1 {proxy_ebs1}")
                                                            st.success(f"referencia {referencia}")
                                                            st.success(f"operacion_legado {operacion_legado}")
                                                            st.success(f"operacion_legado {operacion_legado}")
                                                            
                                                            
                                                            st.success(f"osb_services: {osb_services}")
                                                            
                                                    
                                                    valor_limpio = ""
                                        
                                        else:
                                            osb_file_path = os.path.join(jdeveloper_projects_dir, proxy_interno + ".BusinessService")
                                            project_name = extract_project_name_from_business(osb_file_path)
                                            st.success(f"project_name es : {project_name}")
                                            if project_name is None:
                                                st.success(f"project_name es 'None' : {project_name}")
                                                
                                                continue

                                            with open(osb_file_path, 'r', encoding="utf-8") as f:
                                                content = f.read()
                                                service_name = os.path.splitext(os.path.basename(osb_file_path))[0]
                                                st.success(f"service_name: {service_name}")
                                                wsdl_relative_path = extract_wsdl_relative_path(content)

                                                wsdl_path = os.path.join(jdeveloper_projects_dir, wsdl_relative_path + ".WSDL")
                                                operations = extract_wsdl_operations(wsdl_path)
                                                service_refs = extract_uri_and_provider_id_from_bix(osb_file_path)
                                                st.success(f"service_refs: {service_refs}")
                                                

                                                for uri_value, provider_id_value in service_refs:
                                                    ruta_proxy_completa = proxy_interno
                                                    proxy_ebs3 = referencia.split("/")[-1]
                                                    st.success(f"ruta_proxy_completa {ruta_proxy_completa}")
                                                    st.success(f"proxy_ebs3 {proxy_ebs3}")
                                                    st.success(f"proxy_interno {proxy_interno}")
                                                    st.success(f"DATOS {operacion , proxy_ebs1, proxy_ebs2, proxy_ebs3, ruta_proxy_completa, operacion_legado, uri_value, provider_id_value}")
                                                    osb_services.append((operacion , proxy_ebs1, proxy_ebs2, proxy_ebs3, ruta_proxy_completa, operacion_legado, uri_value, provider_id_value))
                                                    st.success(f"operacion {operacion}")
                                                    st.success(f"proxy_ebs1 {proxy_ebs1}")
                                                    st.success(f"referencia {referencia}")
                                                    st.success(f"operacion_legado {operacion_legado}")
                                                    st.success(f"uri_value {uri_value}")
                                                    st.success(f"provider_id_value {provider_id_value}")
                                                    
                                                    st.success(f"osb_services: {osb_services}")
                                                    
                                            
                                        
                                        st.success(f"osb_services: {osb_services}")
                                        
                                        proxy_ebs3 = ""
                                        

                    elif 'Business' in referencia:
                        st.success("Es BUSINESS SERVICE!!")
                        osb_file_path = os.path.join(jdeveloper_projects_dir, referencia + ".BusinessService")
                        
                        st.success(f"osb_file_path: {osb_file_path}")
                        
                        project_name = extract_project_name_from_business(osb_file_path)
                        st.success(f"project_name: {project_name}")
                        
                        if project_name is None:
                            st.success(f"project_name es 'None' : {project_name}")
                            
                            continue
                            
                        if len(project_name) <= 0:
                            project_name = extract_project_name_from_business_tuxedo(osb_file_path)
                            st.success(f"project_name: {project_name}")
                            
                            
                            service_refs = extract_uri_and_provider_id_from_bix(osb_file_path)
                            st.success(f"service_refs: {service_refs}")
                            

                            for uri_value, provider_id_value in service_refs:
                                osb_services.append((operacion , proxy_ebs1, proxy_ebs2, proxy_ebs3, referencia, operacion_legado, uri_value, provider_id_value))
                                st.success(f"operacion {operacion}")
                                st.success(f"proxy_ebs1 {proxy_ebs1}")
                                st.success(f"proxy_ebs2 {proxy_ebs2}")
                                st.success(f"proxy_ebs3 {proxy_ebs3}")
                                st.success(f"referencia {referencia}")
                                st.success(f"operacion_legado {operacion_legado}")
                                st.success(f"uri_value {uri_value}")
                                st.success(f"provider_id_value {provider_id_value}")
                                
                                st.success(f"osb_services: {osb_services}")
                                

                        with open(osb_file_path, 'r', encoding="utf-8") as f:
                            content = f.read()
                            service_name = os.path.splitext(os.path.basename(osb_file_path))[0]
                            st.success(f"service_name: {service_name}")
                            
                            wsdl_relative_path = extract_wsdl_relative_path(content)
                            st.success(f"wsdl_relative_path: {wsdl_relative_path}")
                            

                            if wsdl_relative_path:
                                wsdl_path = os.path.join(jdeveloper_projects_dir, wsdl_relative_path + ".WSDL")
                                st.success(f"wsdl_path: {wsdl_path}")
                                
                                operations = extract_wsdl_operations(wsdl_path)
                                st.success(f"operations: {operations}")
                                
                                service_refs = extract_uri_and_provider_id_from_bix(osb_file_path)
                                st.success(f"service_refs: {service_refs}")
                                

                                for uri_value, provider_id_value in service_refs:
                                    osb_services.append((operacion , proxy_ebs1, proxy_ebs2, proxy_ebs3, referencia, operacion_legado, uri_value, provider_id_value))
                                    st.success(f"operacion {operacion}")
                                    st.success(f"proxy_ebs1 {proxy_ebs1}")
                                    st.success(f"proxy_ebs2 {proxy_ebs2}")
                                    st.success(f"proxy_ebs3 {proxy_ebs3}")
                                    st.success(f"referencia {referencia}")
                                    st.success(f"operacion_legado {operacion_legado}")
                                    st.success(f"uri_value {uri_value}")
                                    st.success(f"provider_id_value {provider_id_value}")
                                    
                                    st.success(f"osb_services: {osb_services}")
                                    
                    
                    
                else: #Es un ABC
                    if 'Proxies' in referencia:
                        st.success(f"Proxies esta en referencia : {referencia}")
                        
                        osb_file_path = os.path.join(jdeveloper_projects_dir, referencia + ".ProxyService")
                        st.success(f"osb_file_path : {osb_file_path}")
                        
                        project_name = extract_project_name_from_proxy(osb_file_path)
                        if project_name is None:
                            osb_services.append((operacion , proxy_ebs1, proxy_ebs2, proxy_ebs3, referencia, operacion_legado, 'N/A', 'N/A'))
                            st.success(f"project_name es 'None' : {project_name}")
                            
                            
                            st.success(f"osb_services: {osb_services}")
                            
                            continue

                        pipeline_path = extract_pipeline_path_from_proxy(osb_file_path, jdeveloper_projects_dir)
                        st.success(f"pipeline_path: {pipeline_path}")
                        
                        with open(osb_file_path, 'r', encoding="utf-8") as f:
                            content = f.read()
                            service_name = os.path.splitext(os.path.basename(osb_file_path))[0]
                            wsdl_relative_path = extract_wsdl_relative_path(content)

                            if wsdl_relative_path:
                                wsdl_path = os.path.join(jdeveloper_projects_dir, wsdl_relative_path + ".WSDL")
                                st.success(f"wsdl_path: {wsdl_path}")
                                
                                operations = extract_wsdl_operations(wsdl_path)
                                st.success(f"operations: {operations}")
                                
                                service_for_operations = extract_service_for_operations(pipeline_path, operacion_legado)
                                st.success(f"service_for_operations: {service_for_operations}")
                                

                                if not service_for_operations:
                                    service_refs = extract_service_refs_from_pipeline(pipeline_path)
                                    st.success(f"service_for_operations 2: {service_for_operations}")
                                    

                                    for service_ref in service_refs:
                                        osb_services.append((operacion , proxy_ebs1, proxy_ebs2, proxy_ebs3, referencia, operacion_legado, service_ref, operacion_legado))
                                        st.success(f"operacion {operacion}")
                                        st.success(f"proxy_ebs1 {proxy_ebs1}")
                                        st.success(f"referencia {referencia}")
                                        st.success(f"operacion_legado {operacion_legado}")
                                        st.success(f"service_ref {service_ref}")
                                        st.success(f"operacion_legado {operacion_legado}")
                                        
                                        
                                        st.success(f"osb_services: {osb_services}")
                                        

                                else:
                                    for operation, proxy_interno in service_for_operations.items():
                                        st.success(f"operacion {operacion}")
                                        st.success(f"proxy_ebs1 {proxy_ebs1}")
                                        st.success(f"referencia {referencia}")
                                        st.success(f"operacion_legado {operacion_legado}")
                                        st.success(f"proxy_interno {proxy_interno}")
                                        
                                        es_business_service = '/BusinessServices'
                                        if es_business_service not in proxy_interno:
                                        
                                            osb_file_path = os.path.join(jdeveloper_projects_dir, proxy_interno + ".ProxyService")
                                            
                                            st.success(f"osb_file_path {osb_file_path}")
                                            
                                            ruta_pipeline = extract_pipeline_path_from_proxy(osb_file_path, jdeveloper_projects_dir)
                                            st.success(f"ruta_pipeline: {ruta_pipeline}")
                                            if ruta_pipeline is None:
                                                osb_services.append((operacion , proxy_ebs1, proxy_ebs2, proxy_ebs3, referencia, operacion_legado, 'N/A', 'N/A'))
                                                st.success(f"ruta_pipeline es 'None' : {project_name}")
                                                st.success(f"operacion {operacion}")
                                                st.success(f"proxy_ebs1 {proxy_ebs1}")
                                                st.success(f"referencia {referencia}")
                                                st.success(f"operacion_legado {operacion_legado}")
                                                st.success(f"service_ref {service_ref}")
                                                st.success(f"operacion_legado {operacion_legado}")
                                                
                                                
                                                st.success(f"osb_services: {osb_services}")
                                                
                                                continue
                                            operaciones_internas = definir_operaciones_internas_pipeline(ruta_pipeline)
                                            
                                            st.success(f"operaciones_internas {operaciones_internas}")
                                            
                                            for clave in operaciones_internas.keys():
                                                st.success(f"clave {clave}")
                                                
                                                osb_services.append((operacion , proxy_ebs1, proxy_ebs2, proxy_ebs3, referencia, operacion_legado, proxy_interno, clave))
                                                st.success(f"operacion {operacion}")
                                                st.success(f"proxy_ebs1 {proxy_ebs1}")
                                                st.success(f"referencia {referencia}")
                                                st.success(f"operacion_legado {operacion_legado}")
                                                st.success(f"service_ref {service_ref}")
                                                st.success(f"operacion_legado {operacion_legado}")
                                                
                                                
                                                st.success(f"osb_services: {osb_services}")
                                                
                                        
                                        else:
                                            osb_file_path = os.path.join(jdeveloper_projects_dir, proxy_interno + ".BusinessService")
                                            project_name = extract_project_name_from_business(osb_file_path)
                                            st.success(f"project_name es : {project_name}")
                                            if project_name is None:
                                                st.success(f"project_name es 'None' : {project_name}")
                                                
                                                continue

                                            with open(osb_file_path, 'r', encoding="utf-8") as f:
                                                content = f.read()
                                                service_name = os.path.splitext(os.path.basename(osb_file_path))[0]
                                                st.success(f"service_name: {service_name}")
                                                wsdl_relative_path = extract_wsdl_relative_path(content)

                                                wsdl_path = os.path.join(jdeveloper_projects_dir, wsdl_relative_path + ".WSDL")
                                                operations = extract_wsdl_operations(wsdl_path)
                                                service_refs = extract_uri_and_provider_id_from_bix(osb_file_path)
                                                st.success(f"service_refs: {service_refs}")
                                                

                                                for uri_value, provider_id_value in service_refs:
                                                    proxy_ebs2 = proxy_ebs1
                                                    proxy_ebs3 = referencia.split("/")[-1]
                                                    referencia = service_name
                                                    operacion_legado = operation
                                                    st.success(f"DATOS {operacion , proxy_ebs1, proxy_ebs2, proxy_ebs3, proxy_interno, operacion_legado, uri_value, provider_id_value}")
                                                    osb_services.append((operacion , proxy_ebs1, proxy_ebs2, proxy_ebs3, proxy_interno, operacion_legado, uri_value, provider_id_value))
                                                    st.success(f"operacion {operacion}")
                                                    st.success(f"proxy_ebs1 {proxy_ebs1}")
                                                    st.success(f"referencia {referencia}")
                                                    st.success(f"operacion_legado {operacion_legado}")
                                                    st.success(f"uri_value {uri_value}")
                                                    st.success(f"provider_id_value {provider_id_value}")
                                                    
                                                    st.success(f"osb_services: {osb_services}")
                                                    
                                            
                                        
                                        st.success(f"osb_services: {osb_services}")
                                        
                                        

                    elif 'Business' in referencia:
                        st.success("Es BUSINESS SERVICE!!")
                        osb_file_path = os.path.join(jdeveloper_projects_dir, referencia + ".BusinessService")
                        
                        st.success(f"osb_file_path: {osb_file_path}")
                        
                        project_name = extract_project_name_from_business(osb_file_path)
                        st.success(f"project_name: {project_name}")
                        
                        if project_name is None:
                            st.success(f"project_name es 'None' : {project_name}")
                            
                            continue
                            
                        if len(project_name) <= 0:
                            project_name = extract_project_name_from_business_tuxedo(osb_file_path)
                            st.success(f"project_name: {project_name}")
                            
                            
                            service_refs = extract_uri_and_provider_id_from_bix(osb_file_path)
                            st.success(f"service_refs: {service_refs}")
                            

                            for uri_value, provider_id_value in service_refs:
                                osb_services.append((operacion , proxy_ebs1, proxy_ebs2, proxy_ebs3, referencia, operacion_legado, uri_value, provider_id_value))
                                st.success(f"operacion {operacion}")
                                st.success(f"proxy_ebs1 {proxy_ebs1}")
                                st.success(f"proxy_ebs2 {proxy_ebs2}")
                                st.success(f"proxy_ebs3 {proxy_ebs3}")
                                st.success(f"referencia {referencia}")
                                st.success(f"operacion_legado {operacion_legado}")
                                st.success(f"uri_value {uri_value}")
                                st.success(f"provider_id_value {provider_id_value}")
                                
                                st.success(f"osb_services: {osb_services}")
                                

                        with open(osb_file_path, 'r', encoding="utf-8") as f:
                            content = f.read()
                            service_name = os.path.splitext(os.path.basename(osb_file_path))[0]
                            st.success(f"service_name: {service_name}")
                            
                            wsdl_relative_path = extract_wsdl_relative_path(content)
                            st.success(f"wsdl_relative_path: {wsdl_relative_path}")
                            

                            if wsdl_relative_path:
                                wsdl_path = os.path.join(jdeveloper_projects_dir, wsdl_relative_path + ".WSDL")
                                st.success(f"wsdl_path: {wsdl_path}")
                                
                                operations = extract_wsdl_operations(wsdl_path)
                                st.success(f"operations: {operations}")
                                
                                service_refs = extract_uri_and_provider_id_from_bix(osb_file_path)
                                st.success(f"service_refs: {service_refs}")
                                

                                for uri_value, provider_id_value in service_refs:
                                    osb_services.append((operacion , proxy_ebs1, proxy_ebs2, proxy_ebs3, referencia, operacion_legado, uri_value, provider_id_value))
                                    st.success(f"operacion {operacion}")
                                    st.success(f"proxy_ebs1 {proxy_ebs1}")
                                    st.success(f"proxy_ebs2 {proxy_ebs2}")
                                    st.success(f"proxy_ebs3 {proxy_ebs3}")
                                    st.success(f"referencia {referencia}")
                                    st.success(f"operacion_legado {operacion_legado}")
                                    st.success(f"uri_value {uri_value}")
                                    st.success(f"provider_id_value {provider_id_value}")
                                    
                                    st.success(f"osb_services: {osb_services}")
                                    
                    
                    
                    else:
                        osb_services.append((operacion , proxy_ebs1, proxy_ebs2, proxy_ebs3, referencia, operacion_legado, 'N/A', 'N/A'))
                        st.success(f"NO es ni 'Proxy' ni 'Business': {referencia}")
                        
                        st.success(f"osb_services: {osb_services}")
                        
            
            else:
                proxy_interno = referencia.split("/")[-1]
                st.success(f"DATOS {operacion , proxy_ebs1, proxy_ebs2, proxy_interno, referencia, operacion_legado, 'N/A', 'N/A'}")
                osb_services.append((operacion , proxy_ebs1, proxy_ebs2, proxy_interno, referencia, operacion_legado, 'N/A', 'N/A'))
                st.success(f"Palabra invalida: {referencia}")
                
                st.success(f"osb_services: {osb_services}")
                
    return osb_services

def recorrer_y_extraer_operaciones_servicios_osb(project_path,operacion_a_documentar,operations,pipeline_path):
    
    osb_services = []
    st.success(f"project_path: {project_path}")
    st.success(f"operacion_a_documentar: {operacion_a_documentar}")
    st.success(f"operations: {operations}")
    st.success(f"pipeline_path: {pipeline_path}")
    service_for_operations = extract_service_for_operations_audibpel(pipeline_path, operations)
    st.success(f"service_for_operations: {service_for_operations}")
    
    operations_audibpel_exp = {}
    service_for_operations_new = {}

    for operation_name, service_refs in service_for_operations.items():
        for service_ref, exp_name in service_refs:
            
            if ' ' in exp_name or 'N/A' in exp_name:
                # Extraer el nombre del flujo de trabajo de exp_name
                exp_name_cleaned = exp_name  # Obtener 'GestionMediosManejoOficinasVirtualesABC PKG_MEDIOS_MANEJO_OFICINAS_VRT_PR_CONSULTAR_MMAN_OFICINAS_VRT'

                # Construir las nuevas variables
                operations_audibpel_exp[operation_name] = f"{exp_name_cleaned}"
            else:
                # Si no hay espacio en blanco, tomar exp_name completo
                exp_name_cleaned = exp_name

                # Construir las nuevas variables
                operations_audibpel_exp[operation_name] = f"{exp_name_cleaned}"

            if operation_name not in service_for_operations_new:
                service_for_operations_new[operation_name] = []
        
            service_for_operations_new[operation_name].append(service_ref)                                                              

    st.success(f"operations_audibpel_exp: {operations_audibpel_exp}")
    
    st.success(f"service_for_operations_new: {service_for_operations_new}")
    

    service_for_operations = service_for_operations_new
    operaciones_y_ebs = service_for_operations_new
    # Generar los datos en el formato deseado
    service_for_operations_resultado = []
    for operation_name, service_refs in service_for_operations_new.items():
        for service_ref in service_refs:
            service_for_operations_resultado.append({operation_name: service_ref})


    for service_for_operations in service_for_operations_resultado:
        
        st.success(f"service_for_operations: {service_for_operations}")   
        
        referencias_for_operations = extract_osb_services_with_given_path(project_path, service_for_operations)
        st.success("************EXTRACT_OSB_SERVICES_WITH_HTTP_PROVIDER_ID****************")
        
        st.success(f"referencias_for_operations: {referencias_for_operations}")
        
        
        grouped_data = {}
        
        
        # for service, reference in referencias_for_operations:
            # if service not in grouped_data:
                # grouped_data[service] = []
            # grouped_data[service].append(reference)
        
        for key, value in referencias_for_operations:
            grouped_data[key] = value
        
        st.success("************EXTRACT_OSB_SERVICES_WITH_HTTP_PROVIDER_ID****************")
        
        st.success(f"grouped_data: {grouped_data}")
        
        
        for service, references in grouped_data.items():
            st.success(f"{service}: {references}")
        
        st.success("************VERIFICACION GROUPED_DATA****************")
        
        
        grupo_referencia = []
        # Lista para almacenar las claves encontradas
        tuplas_extendidas = []
        
        for operacion, proxies in grouped_data.items():
            if isinstance(proxies, list):
                grupo = {operacion: proxies}
                st.success(grupo)
                st.success("-------------")
                
                if(es_operacion_lista_referencias(grupo)):
                    st.success("grouped_data_1 sigue la estructura del caso 1")
                    
                    
                    for operacion, proxies in grupo.items():
                        for proxy in proxies:
                            grupo_referencia_temporal = []

                            if 'Business' in proxy:
                                
                                st.success(f"El proxy '{proxy}' contiene 'BusinessServices'")
                                servicio = service_for_operations.get(operacion, None)
                                
                                st.success(f"servicio: {servicio}")
                                
                                
                                # Verificar si el servicio es encontrado
                                if servicio:
                                    # Extraer el nombre del servicio de la ruta del servicio
                                    nombre_servicio = servicio.split('/')[-1]
                                    operacion_proxy = proxy.split('/')[-1]
                                    
                                    st.success(f"nombre_servicio: {nombre_servicio}")
                                    
                                    st.success(f"operacion_proxy: {operacion_proxy}")
                                    
                                    
                                    ruta_completa_proxy = os.path.join(project_path, servicio + ".ProxyService")
                                    
                                    if os.path.exists(ruta_completa_proxy):
                                        ruta_completa_pipeline = extract_pipeline_path_from_proxy(ruta_completa_proxy, project_path)
                                        st.success(f"ruta_completa_pipeline: {ruta_completa_pipeline}")
                                        
                                        def_op_internas_pipeline = definir_operaciones_internas_pipeline(ruta_completa_pipeline)
                                        st.success(f"def_op_internas_pipeline: {def_op_internas_pipeline}")
                                        
                                        
                                        operacion_proxy = obtener_operacion_por_proxy(def_op_internas_pipeline, proxy)
                                        
                                        st.success(f"operacion_proxy: {operacion_proxy}")
                                        

                                    tupla_extendida = (operacion,nombre_servicio,proxy,operacion_proxy)
                                    
                                    tuplas_extendidas.append(tupla_extendida)
                                    
                                    st.success(f"tupla_extendida: {tupla_extendida}")
                                    
                                    
                            else:
                                
                                st.success(f"El proxy '{proxy}' no contiene 'BusinessServices'")
                                
                                ruta_completa_proxy = os.path.join(project_path, proxy + ".ProxyService")
                                st.success(f"ruta_completa_proxy: {ruta_completa_proxy}")
                                if os.path.exists(ruta_completa_proxy):
                                    ruta_completa_pipeline = extract_pipeline_path_from_proxy(ruta_completa_proxy, project_path)
                                    st.success(f"ruta_completa_pipeline: {ruta_completa_pipeline}")                                   
                                    operacion_pipeline = extract_service_refs_from_pipeline(ruta_completa_pipeline)
                                    st.success(f"operacion_pipeline: {operacion_pipeline}") 
                                    if not operacion_pipeline:
                                        continue
                                    ruta_completa_wsdl = os.path.join(project_path, devolver_ruta_wsdl_proxy(ruta_completa_proxy) + ".WSDL")
                                    st.success(f"ruta_completa_wsdl: {ruta_completa_wsdl}") 
                                    operaciones_internas = extract_wsdl_operations(ruta_completa_wsdl)
                                    st.success(f"operaciones_internas: {operaciones_internas}")
                                    operacion_pipeline_por_nombre = extract_service_for_operations(ruta_completa_pipeline, operaciones_internas)
                                    st.success(f"operacion_pipeline_por_nombre: {operacion_pipeline_por_nombre}")
                                    def_op_internas_pipeline = definir_operaciones_internas_pipeline(ruta_completa_pipeline)
                                    st.success(f"def_op_internas_pipeline: {def_op_internas_pipeline}")
                                
                                    referencia_operacion = {operacion: proxy}
                                    st.success(f"referencia_operacion: {referencia_operacion}")
                                    grupo_referencia_temporal.append(referencia_operacion)
                                    
                                    referencias_for_operations = extract_osb_services_with_given_path_dict(project_path, grupo_referencia_temporal)
                                    
                                    st.success("************GRUPO_REFERENCIA****************")
                                    
                                    st.success(f"referencias_for_operations GRUPO: {referencias_for_operations}")
                                    
                                    # st.success("************GRUPO_REFERENCIA****************")
                                    
                                    # grupo_referencia.append(referencias_for_operations)
                                    


                                    # Iterar sobre cada tupla en referencias_for_operations
                                    for tupla in referencias_for_operations:
                                        # Obtener el valor de la tercera posición de la tupla
                                        valor_tercera_posicion = tupla[2]
                                        # Verificar si este valor está en def_op_internas_pipeline
                                        if valor_tercera_posicion in def_op_internas_pipeline.values():
                                            # Si está, encontrar la clave correspondiente en def_op_internas_pipeline
                                            clave_encontrada = next(key for key, value in def_op_internas_pipeline.items() if value == valor_tercera_posicion)
                                            # Extender la tupla con la clave encontrada
                                            tupla_extendida = tupla + (clave_encontrada,)
                                            # Agregar la tupla extendida a la lista
                                            tuplas_extendidas.append(tupla_extendida)
                                            
                                            st.success(f"tupla_extendida: {tupla_extendida}")


                                    
                                    
                                    

                if es_operacion_clave_valor(grupo):
                    st.success("grouped_data_2 sigue la estructura del caso 2")
                
            else:
                # Si los proxies no son una lista, imprimimos la operación y el proxy directamente
                st.success({operacion: proxies})
                st.success("-------------")
                
                
        
        # st.success(f"grupo_referencia: {grupo_referencia}")
        
        st.success("************VERIFICACION GROUPED_DATA****************")
        
        
        st.success(f"tuplas_extendidas: {tuplas_extendidas}")
        
        referencias_abc2 = extract_osb_services_references_abc2(project_path, tuplas_extendidas)
        
        
        
        # referencias_abc = extract_osb_services_references_abc(project_path, grupo_referencia)
        
        #referencias_finales = extract_osb_services_finals(project_path, grouped_data)
        
        st.success("************EXTRACT_OSB_SERVICES_WITH_HTTP_PROVIDER_ID****************")
         
        
        
        st.success("-----------------INFO-----------------------")
        st.success(f"project_name: {project_name}")
        
        st.success(f"service_name: {service_name}")
        
        st.success(f"service_url: {service_url}")
        
        st.success(f"operations: {operations}")
        
        st.success(f"pipeline_path: {pipeline_path}")
        
        st.success(f"operacion_proxy: {service_for_operations}")
        
        st.success(f"grouped_data: {grouped_data}")
        
        st.success(f"grupo_referencia: {grupo_referencia}")
        
        st.success(f"referencias_abc2: {referencias_abc2}")
        
        st.success(f"tuplas_extendidas: {tuplas_extendidas}")
        
        st.success(f"operations_audibpel_exp: {operations_audibpel_exp}")                                                                                                    
        st.success("-----------------INFO-----------------------")
        
        
        
        
        st.success("-----------------INICIO ANALISIS-----------------------")
        
        
        
        # Lista para almacenar los resultados
        for index, referencia in enumerate(referencias_abc2, start=1):
            operacion_abc = referencia[0]
            proxy_ebs_completo = service_for_operations.get(operacion_abc)
            parts_proxy = proxy_ebs_completo.split('/')
            ruta_proxy_ebs = parts_proxy[0]
            nombre_ebs = operaciones_y_ebs.get(operacion_abc, None)
            st.success(f"nombre_ebs: {nombre_ebs}")  
            cadena = nombre_ebs[0]
            proxy_ebs1 = cadena.split("/")[-1]
            proxy_ebs2 = referencia[2]
            proxy_ebs3 = referencia[3]
            num_barras = proxy_ebs3.count("/")
            
            if num_barras >= 1:
                indice_ultimo = proxy_ebs3.rfind("/")
                if indice_ultimo != -1:
                    proxy_abc =  proxy_ebs3[indice_ultimo + 1:]
                    proxy_ebs3 = proxy_ebs3[:indice_ultimo]
            else:
                proxy_abc = referencia[3]

            ruta_business_completa = referencia[4]
            nombre_flujo_audibpel_exp = operations_audibpel_exp.get(operacion_abc)                                                                      
            
            parts_business = ruta_business_completa.split('/')
            proyecto_abc = parts_business[0]
            nombre_business = parts_business[-1]
            
            if 'PS' not in proxy_abc and 'RegistrarAuditoriaSOADATV1.0' not in proxy_abc:
                proxy_abc = nombre_business
            
            url_business = referencia[6]
            tipo_business = referencia[7]
            operacion_business = referencia[5]
            
            datos = f"({index},'{service_name}','{operacion_abc}','{project_name}','{service_url}','{nombre_flujo_audibpel_exp}','{ruta_proxy_ebs}','{proxy_ebs1}','{proxy_ebs2}','{proxy_ebs3}','{proxy_abc}', '{proyecto_abc}', '{nombre_business}','{operacion_business}', '{url_business}', '{tipo_business}')"
            
            st.success(f"({datos})")
            
            osb_services.append(datos)
        
        st.success("************EXTRACT_OSB_SERVICES_WITH_HTTP_PROVIDER_ID****************")
        st.success(f"OSB: {osb_services}")
                                
    return osb_services

def generar_documentacion(jar_path, plantilla_path,operacion_a_documentar,nombre_autor):
    """Función que ejecuta la generación de documentación."""
    
    zip_files = []
    generoArchivo = False
    
    # Extraer ruta del proyecto desde el .jar
    jdeveloper_projects_dir = jar_path
    
    #st.success(f"✅ jdeveloper_projects_dir {jdeveloper_projects_dir}")
    
    if not jdeveloper_projects_dir:
        st.error("No se pudo determinar la ruta del proyecto desde el .jar.")
        return

    # 📌 Definir la ruta del directorio temporal correctamente
    temp_dir = os.path.join(tempfile.gettempdir(), "documentacion_osb")
    ruta_temporal = temp_dir  # Obtener la ruta temporal

    if not isinstance(temp_dir, str) or not temp_dir:
        st.error("⛔ Error: La ruta temporal no es válida.")
    else:
        # 📌 Verificar si la carpeta existe antes de intentar eliminarla
        if os.path.exists(temp_dir):
            try:
                shutil.rmtree(temp_dir)  # 🔥 Borra todo el contenido anterior
                #st.warning("📂 Se limpiaron los archivos temporales previos.")
            except Exception as e:
                st.error(f"⛔ No se pudo eliminar la carpeta temporal: {e}")

        # 📌 Crear nuevamente la carpeta temporal limpia
        os.makedirs(temp_dir, exist_ok=True)
        #st.success(f"📂 Carpeta temporal creada: {temp_dir}")
    
    # Llamar a la función principal de tu script
    services_with_data = extraer_schemas_operaciones_expuestas_http(jdeveloper_projects_dir,operacion_a_documentar)
    
    sys.stdout.write(f"✅ services_with_data {services_with_data}")
    
    es_type = False
    
    # Initialize an empty set to store unique operation names
    operation_names = set()
    
    if services_with_data:

        # Iterate through each tuple of request and response elements in services_with_data
        for request_elements, response_elements in services_with_data:
            # Iterate through each element in request_elements and response_elements
            for element in request_elements + response_elements:
                if 'Type' in element['elemento']:
                    es_type = True
                #operation_name = element['elemento'].replace('Request', '').replace('Response', '').replace('Type', '')
                ##st.success(f"operation_name: {operation_name}")
                service_name = element['service_name']
                # Agregar todas las operaciones de la lista 'operations'
                if 'operations' in element:
                    operation_names.update(element['operations'])  # Agrega todas las operaciones a operation_names

        # Convert the set to a sorted list to get the operation names in alphabetical order
        unique_operations = sorted(operation_names)
        
        operaciones_formateadas = "\n".join(f"* {op}" for op in unique_operations)
        
        
        # 🔹 Si operacion_a_documentar tiene un valor, filtrar solo esa operación
        if operacion_a_documentar:
            unique_operations = [operacion_a_documentar] if operacion_a_documentar in unique_operations else []
            
        
        #st.success(f"unique_operations: {unique_operations}")
        
        #st.success(f"✅ unique_operations {unique_operations}")
        
        operation_elements = {}
        
        
        total_operaciones = len(unique_operations)
        if total_operaciones == 0:
            st.warning("⚠️ No hay operaciones que documentar.")
            return
        
        if total_operaciones > 1:
            progress_bar_general = st.progress(0)
        
        # 🔹 Iterar sobre cada operación
        for idx, operation in enumerate(unique_operations, start=1):
            if total_operaciones > 1:
                progreso_actual = int((idx / total_operaciones) * 100)
                progress_bar_general.progress(progreso_actual)  # 🔄 Actualizar barra general
                #st.success(f"⏳ Procesando operación {idx}/{total_operaciones}: {operation} ({progreso_actual}%)")
            else:
                st.success(f"⏳ Procesando operación {idx}/{total_operaciones}: {operation}")
            
            
            if es_type:
                request_key = f"{operation}RequestType"
                response_key = f"{operation}ResponseType"
            else:
                request_key = f"{operation}Request"
                response_key = f"{operation}Response"
            
            # Initialize lists to store request and response elements for the current operation
            request_elements = []
            response_elements = []
            url_elements = []
            capa_proyecto = []
            minOccurs_elements = []
            
            # Iterate through services_with_data to find matching elements
            for request_data, response_data in services_with_data:
                #st.success(f"request_data: {request_data}")
                # Check for request elements
                for element in request_data:
                    elemento_nombre = element['elemento']
                    # ✅ Verificar coincidencia exacta o parcial usando difflib
                    match = difflib.get_close_matches(request_key, [elemento_nombre], n=1, cutoff=0.9)
                    
                    if match or request_key in elemento_nombre:  # Si hay coincidencia razonable
                        request_elements.append({'name': element['name'], 'type': element['type'],'minOccurs': element['minOccurs']})
                        url_elements.append({'url': element['url']})
                        capa_proyecto.append({'ruta': element['ruta']})
                        minOccurs_elements.append({'minOccurs': element['minOccurs']})
                        service_name = element['service_name']
                
                # 🔹 Verificar si `response_key` está en `response_data['elemento']`
                for element in response_data:
                    elemento_nombre = element['elemento']

                    # ✅ Verificar coincidencia exacta o parcial
                    match = difflib.get_close_matches(response_key, [elemento_nombre], n=1, cutoff=0.9)
                    
                    if match or response_key in elemento_nombre:  
                        response_elements.append({'name': element['name'], 'type': element['type'],'minOccurs': element['minOccurs']})
                        service_name = element['service_name']
            
            # Store the collected elements in the dictionary
            operation_elements[operation] = {
                'request': request_elements,
                'response': response_elements,
                'url': url_elements,
                'ruta': capa_proyecto, 
                'minOccurs': minOccurs_elements,
                'service_name': service_name
            }
            
        #st.success(f"operation_elements: {operation_elements}")
        ##st.success(f"service_name: {service_name}")
        # Print the result
        # 📂 Crear un solo ZIP para todas las operaciones
        zip_buffer = tempfile.NamedTemporaryFile(delete=False, suffix=".zip")
        zip_path = zip_buffer.name  # Ruta del archivo ZIP
        
        with zipfile.ZipFile(zip_path, "w", zipfile.ZIP_DEFLATED) as zipf:
            for idx, (operation, elements) in enumerate(operation_elements.items(), start=1):
                
                #st.write(f"🔹 Procesando operación: {operation}")
                st.write(f"📌 Cantidad de elementos request: {len(elements['request'])}")
                st.write(f"📌 Cantidad de elementos response: {len(elements['response'])}")

                #st.success(f"elements['request']: {elements['request']}")
                if not elements['request']:
                    st.warning(f"⚠️ La operación {operation} no tiene elementos de entrada, saltando...")
                    continue  # Si no hay request, no genera el documento

                # 🔹 Actualizar progreso de generación de documentos
                if total_operaciones > 1:
                    progreso_actual = int(((idx + total_operaciones) / (total_operaciones * 2)) * 100)
                    progress_bar_general.progress(progreso_actual)

                if elements['request']:
                    
                    st.write(f"🔹 Proyecto {elements['ruta'][0]['ruta'].lstrip('/')}")
                    st.write(f"⏳ Creando documentacion operacion: {operation}")
                    
                    #if total_operaciones == 1:
                        #progress_bar_general = st.progress(2)
                    
                    contiene_cabecera_entrada = False
                    contiene_cabecera_salida = False
                    
                    if any('cabeceraEntrada.' in elem['name'] for elem in elements['request']):
                        #st.write("Se encontró al menos un elemento con '.cabeceraEntrada.'")
                        contiene_cabecera_entrada = True
                    
                    if any('cabeceraSalida.' in elem['name'] for elem in elements['response']):
                        #st.write("Se encontró al menos un elemento con '.cabeceraSalida.'")
                        contiene_cabecera_salida = True
                        
                    # Cargar el documento de la plantilla
                    doc = Document(plantilla_path)
                    
                    # Contar el número de tablas en el documento
                    num_tables = len(doc.tables)
                    
                    #st.success(f"El documento contiene {num_tables} tabla(s).")

                    # Mostrar cada tabla
                    for i, table in enumerate(doc.tables):
                        #st.success(f"\nTabla {i+1}:")
                        for row in table.rows:
                            row_data = [cell.text for cell in row.cells]
                            st.success('\t'.join(row_data))
                    
                    url = ""
                    ruta =""
                    minOccurs = ""
                    
                    for elem in elements['url']:
                        url = elem['url']
                        
                    for elem in elements['ruta']:
                        ruta = elem['ruta']
                    
                    for elem in elements['minOccurs']:
                        minOccurs = elem['minOccurs']
                        
                    #st.success(f"url: {url}")
                    
                    #st.success(f"ruta: {ruta}")
                    
                    #st.success(f"business: {business}")
                    
                    fecha_actual = datetime.now()
                    fecha_formateada = fecha_actual.strftime("%d/%m/%Y")
                    
                    
                    
                    #st.success(f"operation: {operation}")
                    
                    #st.success(f"elements: {elements}")
                    
                    
                    
                    # Definir las variables y sus valores
                    variables = {
                        '{nombre_servicio_inicial}': service_name,
                        '{nombre_servicio_secundario}': service_name,
                        '{nombre_servicio}': service_name,
                        '{nombre_operacion_inicial}' : operation,
                        '{nombre_operacion}': operation,
                        '{unique_operations}': operaciones_formateadas,
                        '{nombre_servicio_contrato}': service_name,
                        '{nombre_servicio_wsdl}': service_name,
                        '{nombre_servicio_contrato2}': service_name,
                        '{nombre_servicio_tabla}': operation,
                        '{fecha}': fecha_formateada,
                        '{autor_inicial}': nombre_autor,
                        '{autor}': nombre_autor,
                        '{autor2}': 'Julian Orjuela',
                        '{url}': url,
                        '{operacion_legado}': minOccurs,
                        '{proyecto_abc}': 'TENENCIA_COMPORTAMIENTO_ABC'
                        # Añade más variables según sea necesario
                    }
                    #st.success(f"service_name: {service_name}")
                    #st.success(f"variables: {variables}")
                    
                    total_tablas = len(doc.tables)
                    #st.success(f"🔍 Total de tablas en el documento: {total_tablas}")
                    if total_operaciones == 1:
                        progress_bar_general = st.progress(30)
                    
                    tabla_cabecera_entrada_numero = 4
                    tabla_cabecera_entrada = doc.tables[tabla_cabecera_entrada_numero - 1]  # Las tablas se indexan desde 0, por eso restamos 1

                    tabla_request_numero = 5
                    tabla_request = doc.tables[tabla_request_numero - 1]  # Las tablas se indexan desde 0, por eso restamos 1
                    
                    tabla_cabecera_salida_numero = 6
                    tabla_cabecera_salida = doc.tables[tabla_cabecera_salida_numero - 1]  # Las tablas se indexan desde 0, por eso restamos 1
                    
                    tabla_response_numero = 7
                    tabla_response = doc.tables[tabla_response_numero - 1]  # Las tablas se indexan desde 0, por eso restamos 1
                    
                    if tabla_cabecera_salida_numero > total_tablas:
                        st.error(f"⛔ Error: Se intentó acceder a la tabla {tabla_cabecera_salida_numero}, pero el documento solo tiene {total_tablas} tablas.")
                        return  # Salir para evitar el error
                    
                    # Listas para almacenar las filas de cada subtabla
                    cabecera_salida = []
                    datos_respuesta = []
                    
                    # Variables de control
                    seccion_actual = None
                    
                    #st.success(f"Número total de tablas en el documento: {len(doc.tables)}")
                    
                    for i, table in enumerate(doc.tables):
                        #st.success(f"Tabla {i + 1}:")  # Mostrar el número de la tabla

                        for row in table.rows:
                            row_text = [cell.text.strip() for cell in row.cells]  # Extraer el texto de cada celda
                            #st.success(f"  {row_text}")  # Imprimir el contenido de la fila

                        st.success("-" * 50)  # Separador entre tablas
                   
                   
                    # Recorrer las filas de la tabla 7
                    # for row in tabla_cabecera_salida.rows:
                        # row_text = [cell.text.strip() for cell in row.cells]

                        # # Detectar la cabecera de cada subtabla
                        # if "CabeceraSalida" in row_text:
                            # seccion_actual = "cabecera_salida"
                            # continue  # Saltar a la siguiente fila

                        # if "Response Body" in row_text:
                            # seccion_actual = "datos_respuesta"
                            # continue  # Saltar a la siguiente fila

                        # # Guardar las filas en la subtabla correspondiente
                        # if seccion_actual == "cabecera_salida":
                            # cabecera_salida.append(row_text)

                        # elif seccion_actual == "datos_respuesta":
                            # datos_respuesta.append(row_text)
                   
                    # # Identificar la sección "Datos Respuesta"
                    # for row in tabla_cabecera_salida.rows:
                        # if "Response Body" in row.cells[0].text:
                            # tabla_response = tabla_cabecera_salida  # Ahora sí es una tabla válida
                            # break
                    # else:
                        # st.success("No se encontró la sección 'Response Body' en la tabla 7.")
                        # tabla_response = None  # Para evitar futuros errores
                   
                    
                    # Datos por defecto para LONGITUD y OBSERVACIÓN
                    default_longitud = "default"
                    default_observacion = ""
                    
                    # Limpiar la tabla antes de agregar elementos de esta operación
                    if not contiene_cabecera_entrada:
                        tbl = tabla_cabecera_entrada._element
                        tbl.getparent().remove(tbl)
                        while len(tabla_cabecera_entrada.rows) > 1:
                            tabla_cabecera_entrada._element.remove(tabla_cabecera_entrada.rows[1]._element)
                            
                    # Limpiar la tabla antes de agregar elementos de esta operación
                    if not contiene_cabecera_salida:
                        tbl = tabla_cabecera_salida._element
                        tbl.getparent().remove(tbl)
                        while len(tabla_cabecera_salida.rows) > 1:
                            tabla_cabecera_salida._element.remove(tabla_cabecera_salida.rows[1]._element)
                    
                    # Limpiar la tabla antes de agregar elementos de esta operación
                    while len(tabla_cabecera_entrada.rows) > 2:
                        tabla_cabecera_entrada._element.remove(tabla_cabecera_entrada.rows[2]._element)
                        
                    # Limpiar la tabla antes de agregar elementos de esta operación
                    while len(tabla_cabecera_salida.rows) > 2:
                        tabla_cabecera_salida._element.remove(tabla_cabecera_salida.rows[2]._element)

                    # Limpiar la tabla antes de agregar elementos de esta operación
                    while len(tabla_request.rows) > 2:
                        tabla_request._element.remove(tabla_request.rows[2]._element)
                        
                    # Limpiar la tabla antes de agregar elementos de esta operación
                    while len(tabla_response.rows) > 2:
                        tabla_response._element.remove(tabla_response.rows[2]._element)
                    
                    # Procesar los datos
                    for elem in elements['request']:
                        
                        obligatorio = "NO"
                        #if 'cabeceraEntrada.' not in elem['name']:
                        # Añadir una nueva fila al final de la tabla
                        #fila[0].text = operation + "Request" + "." + elem['name']
                        if 'cabeceraEntrada' in elem['name']:
                            fila_cabecera_entrada = tabla_cabecera_entrada.add_row().cells
                            fila_cabecera_entrada[0].text = elem['name']
                            #st.success(f"fila[0].text: {fila[0].text}")
                            fila_cabecera_entrada[1].text = elem['name']
                            campo = fila_cabecera_entrada[1].text.split('.')[-1]
                            fila_cabecera_entrada[1].text = campo
                            #st.success(f"fila[1].text: {fila[1].text}")
                            if elem['minOccurs'] == '1':
                                obligatorio = "SI"
                            fila_cabecera_entrada[2].text = obligatorio
                            fila_cabecera_entrada[3].text = elem['type']
                            tipo_campo = fila_cabecera_entrada[3].text.split(':')[-1]
                            if tipo_campo == 'string':
                                tipo_campo = 'String'
                            fila_cabecera_entrada[3].text = tipo_campo
                        else:
                            fila = tabla_request.add_row().cells
                            fila[0].text = elem['name']
                            #st.success(f"fila[0].text: {fila[0].text}")
                            fila[1].text = elem['name']
                            campo = fila[1].text.split('.')[-1]
                            fila[1].text = campo
                            #st.success(f"fila[1].text: {fila[1].text}")
                            if elem['minOccurs'] == '1':
                                obligatorio = "SI"
                            fila[2].text = obligatorio
                            fila[3].text = elem['type']
                            tipo_campo = fila[3].text.split(':')[-1]
                            if tipo_campo == 'string':
                                tipo_campo = 'String'
                            fila[3].text = tipo_campo
                        #st.success(f"fila[3].text: {fila[3].text}")
                    
                    if total_operaciones == 1:
                        progress_bar_general.progress(50)
                    
                    # Limpiar la tabla antes de agregar elementos de esta operación
                    while len(tabla_response.rows) > 2:
                        tabla_response._element.remove(tabla_response.rows[2]._element)
                    
                    # Procesar los datos
                    for elem in elements['response']:
                        
                        obligatorio = "NO"
                        #if 'cabeceraSalida.' not in elem['name']:
                        # Añadir una nueva fila al final de la tabla
                        # Rellenar la fila con los datos correspondientes
                        #fila[0].text = operation + "Response" + "." + elem['name']
                        if 'cabeceraSalida' in elem['name']:
                            fila_cabecera_salida = tabla_cabecera_salida.add_row().cells
                            fila_cabecera_salida[0].text = elem['name']
                            #st.success(f"fila[0].text: {fila[0].text}")
                            fila_cabecera_salida[1].text = elem['name']
                            campo = fila_cabecera_salida[1].text.split('.')[-1]
                            fila_cabecera_salida[1].text = campo
                            #st.success(f"fila[1].text: {fila[1].text}")
                            if elem['minOccurs'] == '1':
                                obligatorio = "SI"
                            fila_cabecera_salida[2].text = obligatorio
                            fila_cabecera_salida[3].text = elem['type']
                            tipo_campo = fila_cabecera_salida[3].text.split(':')[-1]
                            if tipo_campo == 'string':
                                tipo_campo = 'String'
                            fila_cabecera_salida[3].text = tipo_campo
                        else:
                            fila = tabla_response.add_row().cells
                            fila[0].text = elem['name']
                            #st.success(f"fila[0].text: {fila[0].text}")
                            fila[1].text = elem['name']
                            campo = fila[1].text.split('.')[-1]
                            fila[1].text = campo
                            #st.success(f"fila[1].text: {fila[1].text}")
                            if elem['minOccurs'] == '1':
                                obligatorio = "SI"
                            fila[2].text = obligatorio
                            fila[3].text = elem['type']
                            tipo_campo = fila[3].text.split(':')[-1]
                            if tipo_campo == 'string':
                                tipo_campo = 'String'
                            fila[3].text = tipo_campo
                    
                    if total_operaciones == 1:
                        progress_bar_general.progress(75)
                    
                    st.success("___________________________________________")
                    
                    #st.success(f"✅ temp_dir  {temp_dir }")
                    #st.success(f"✅ ruta_temporal  {ruta_temporal }")

                    # Lista para almacenar las rutas de los documentos generados
                    documentos_generados = []

                    ruta_proyecto = ruta.strip("/")  # Asegurar que la ruta no tenga "/" al inicio
                    #st.success(f"✅ ruta_proyecto  {ruta_proyecto }")
                    nombre_documento = f"Especificación Servicio WSDL {operation}.docx"
                    
                    # Crear la ruta dentro de la carpeta temporal
                    carpeta_destino = os.path.join(ruta_temporal, ruta_proyecto)
                    os.makedirs(carpeta_destino, exist_ok=True)  # Crear la carpeta si no existe
                    
                    ruta_guardado = os.path.join(carpeta_destino, nombre_documento)
                    
                    doc_nuevo = replace_text_in_doc(doc, variables)
                    doc_nuevo.save(ruta_guardado)  # Guardar en la carpeta temporal
                    st.success(f"📄 Documento generado: ✅ {nombre_documento}")
                    
                    if total_operaciones == 1:
                        progress_bar_general.progress(100)
                    
                    
                    # 📌 Agregar el documento al ZIP
                    if os.path.exists(ruta_guardado):
                        zipf.write(ruta_guardado, os.path.join(ruta_proyecto, nombre_documento))
                        #st.success(f"📄 Documento agregado al ZIP: {ruta_guardado}")
                    else:
                        st.warning(f"⚠️ Documento no encontrado: {ruta_guardado}")
                    
                    generoArchivo = True
                        
        # 📥 Permitir la descarga del ZIP final
        with open(zip_path, "rb") as file:
            zip_bytes = file.read()
        
        progress_bar_general.progress(100)  # ¡Completado!
        st.success("Documentación generada con éxito!")

        # 🔹 Agregar un pequeño delay para asegurar que el ZIP esté listo
        time.sleep(2)  # Esperar 2 segundos antes de mostrar la descarga

        # 🔹 Descargar automáticamente el ZIP sin necesidad de clic
        st.download_button(
            label="📥 Descargar TODOS los documentos en ZIP",
            data=zip_bytes,
            file_name="Documentos_Completos.zip",
            mime="application/zip",
            key="download_all",
        )


def obtener_operaciones(project_path):

    operations =[]
    for root, dirs, files in os.walk(project_path):
        if os.path.basename(root) == "Proxies":
            ##st.success(f"✅ Proxies {elementos_xsd}")
            for file in files:
                if file.endswith('.ProxyService'):
                    osb_file_path = os.path.join(root, file)
                    #st.success(f"✅ osb_file_path {osb_file_path}")
                    project_name = extract_project_name_from_proxy(osb_file_path)
                    
                    if project_name is None:
                        continue 
                    pipeline_path = extract_pipeline_path_from_proxy(osb_file_path, project_path)
                    ##st.success(f"✅ pipeline_path {pipeline_path}")
                    with open(osb_file_path, 'r', encoding="utf-8") as f:
                        content = f.read()
                        if has_http_provider_id(content):
                            service_name = os.path.splitext(file)[0]
                            service_url = extract_service_url(content)
                            wsdl_relative_path = extract_wsdl_relative_path(content)
                            operacion_business = ""
                            if wsdl_relative_path:
                                wsdl_path = os.path.join(project_path, wsdl_relative_path + ".WSDL")
                                capa_proyecto = '/'+ wsdl_relative_path.split('/')[0]
                                
                                #st.success(f"capa_proyecto: {capa_proyecto}")
                                
                                #st.success(f"wsdl_path: {wsdl_path}")
                                operaciones_especificas = extract_wsdl_operations(wsdl_path)
                                #st.success(f"operations: {operations}")
                                
                                for operation in operaciones_especificas:
                                    operations.append(operation)
    return operations


def main():
    st.markdown(
    "<h1 style='text-align: center;'>📄 Generador de Documentación OSB</h1>",
    unsafe_allow_html=True)
    
    # Ruta donde se extraerán los archivos
    carpeta_destino = "extraccion_jar"
    operacion_a_documentar = ""
    
    # 📌 Agregar elementos al menú lateral
    with st.sidebar:
        jar_file = st.file_uploader("Sube el archivo .jar con dependencias", type=["jar"])
        plantilla_file = st.file_uploader("Sube la plantilla de Word", type=["docx"])
        if jar_file:
            jar_path = "temp.jar"

            # 🔥 Borrar contenido previo de la carpeta `extraccion_jar` solo si existe
            if os.path.exists(carpeta_destino):
                try:
                    shutil.rmtree(carpeta_destino)  # Elimina la carpeta y su contenido
                except Exception as e:
                    st.success(f"⚠️ No se pudo limpiar la carpeta temporal: {e}")

            # 📌 Crear nuevamente la carpeta vacía
            os.makedirs(carpeta_destino, exist_ok=True)

            # Guardar el nuevo archivo .jar
            with open(jar_path, "wb") as f:
                f.write(jar_file.getbuffer())

            # 📂 Extraer los archivos del nuevo .jar
            try:
                with zipfile.ZipFile(jar_path, "r") as jar:
                    jar.extractall(carpeta_destino)
                    archivos_extraidos = jar.namelist()

                #st.success(f"✅ Archivos extraídos en: {carpeta_destino}")
            except zipfile.BadZipFile:
                st.error("❌ Error: El archivo no es un JAR válido o está dañado.")
            
            operaciones = obtener_operaciones(carpeta_destino)
            # Agregar una opción vacía al inicio de la lista
            operaciones.insert(0, "TODAS")
            if operaciones:  # Solo mostrar si hay operaciones disponibles
                operacion_a_documentar = st.selectbox("Selecciona una operación", operaciones)
                if operacion_a_documentar == "TODAS":
                    operacion_a_documentar = None
            else:
                st.warning("⚠️ No se encontraron operaciones disponibles.")
                operacion_a_documentar = None  # Para evitar errores si está vacío           
        nombre_autor = st.text_input("Nombre del autor", value="Kevin Torres")  # Valor por defecto
        generar_doc = st.button("Generar Documentación")
         
    with st.container():
        if generar_doc:
            if jar_file and plantilla_file and nombre_autor:
                #st.success(f"✅ operacion_a_documentar: {operacion_a_documentar}")
                with st.spinner("Generando documentación..."):
                    generar_documentacion(carpeta_destino, plantilla_file,operacion_a_documentar,nombre_autor)
            else:
                st.error("Por favor, sube todos los archivos, escribe el autor y proporciona la ruta de destino.")
                

if __name__ == "__main__":
    main()
