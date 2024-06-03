# tallerSQL

## Diagrama ER
![image](https://github.com/10075016-22/tallerSQL/assets/11299320/f638e0c8-1132-475c-b9bd-d61fb033cacb)

## Creación de base de datos
Antes de realizar la creación del esquema es indispensable crear la base de datos donde se definirán las tablas, para almacenar los datos con los que realizaremos las consultas.

```sql
CREATE DATABASE taller;
```
La base de datos puede tener el nombre que queramos, luego de este paso, haremos uso de esta de la siguiente manera: 
```sql
USE taller;
```
## Creación de tablas

```sql
CREATE TABLE sis_tipo_documentos (
    id INT NOT NULL IDENTITY PRIMARY KEY,
    tipo_documento VARCHAR(100) NOT NULL,
    descripcion VARCHAR(100) NULL
);

CREATE TABLE sis_tipo_usuarios (
	id int NOT NULL IDENTITY PRIMARY KEY,
	tipo_usuario varchar(100) NOT NULL
);

CREATE TABLE sis_fondo_pension (
	id int NOT NULL IDENTITY PRIMARY KEY,
	fondo_pension varchar(100) NULL
);

CREATE TABLE sis_arp (
	id int NOT NULL IDENTITY PRIMARY KEY,
	arp varchar(100) NOT NULL
);

CREATE TABLE sis_estado_afiliacion (
	id int NOT NULL IDENTITY PRIMARY KEY,
	estado varchar(100) NOT NULL
);

CREATE TABLE sis_regimen (
	id int NOT NULL IDENTITY PRIMARY KEY,
	regimen varchar(100) NOT NULL,
	descripcion varchar(250) NULL
);

CREATE TABLE sis_tipo_empleado (
	id int NOT NULL IDENTITY PRIMARY KEY,
	tipo_empleado varchar(150) NOT NULL,
	descripcion varchar(250) NULL
);

CREATE TABLE sis_eps (
	id int NOT NULL IDENTITY PRIMARY KEY,
	entidad varchar(150) NOT NULL,
	codigo varchar(250) NOT NULL,
	nit BIGINT NOT NULL
);

CREATE TABLE sis_usuarios (
	id int NOT NULL IDENTITY PRIMARY KEY,
	usuario varchar(150) NOT NULL,
	contraseña varchar(250) NOT NULL,
	nombre_completo varchar(250) NOT NULL,
	ultimo_acceso DATETIME NOT NULL,
    estado TINYINT DEFAULT 1
);

CREATE TABLE sis_especialidades (
	id int NOT NULL IDENTITY PRIMARY KEY,
	especialidad varchar(150) NOT NULL,
	codigo VARCHAR(100) NOT NULL
);

CREATE TABLE sis_tipo_medico (
	id int NOT NULL IDENTITY PRIMARY KEY,
	tipo varchar(150) NOT NULL
);

CREATE TABLE sis_servicios (
	id int NOT NULL IDENTITY PRIMARY KEY,
	servicio varchar(150) NOT NULL
);

CREATE TABLE escolaridades (
	id int NOT NULL IDENTITY PRIMARY KEY,
	nivel_escolaridad varchar(100) NULL
);


CREATE TABLE ocupaciones (
	id int NOT NULL IDENTITY PRIMARY KEY,
	ocupacion varchar(100) NULL
);

CREATE TABLE departamentos (
	id int NOT NULL IDENTITY PRIMARY KEY,
	departamento varchar(100) NULL
);

CREATE TABLE ciudades (
	id int NOT NULL IDENTITY PRIMARY KEY,
	ciudad varchar(100) NULL,
	departamento_id int,
	FOREIGN KEY (departamento_id) REFERENCES departamentos(id)
);

CREATE TABLE sis_paciente (
	id int NOT NULL IDENTITY PRIMARY KEY,
	tipo_id INT,
	num_id BIGINT NOT NULL UNIQUE,
	carnet BIGINT NOT NULL, 
	tipo_usuario INT,
	primer_ape VARCHAR(100) NOT NULL,
	segundo_ape VARCHAR(100) NOT NULL,
	primer_nom VARCHAR(100) NOT NULL,
	segundo_nom VARCHAR(100) NULL,
	fecha_naci DATE NOT NULL,
	sexo CHAR NOT NULL,
	tipo_sangre VARCHAR(2) NOT NULL,
	cod_ciudad INT,
	zona VARCHAR(10) NOT NULL,
	direccion VARCHAR(200) NOT NULL DEFAULT ('N/A'),
	barrio VARCHAR (100) NOT NULL,
	telefono VARCHAR(10) NULL,
	tipo_afilia INT,
	cod_usuario INT,
	nombre_padre VARCHAR NULL,
	nombre_madre VARCHAR NULL,
	conyugue VARCHAR NULL,
	fecha_crea DATETIME,
	ocupacion_id INT,
	cargo VARCHAR(100) DEFAULT 'N/A',
	fecha_ultima_atencion DATE NULL,
	sem_cot INT,
	est_afil_id INT,
	tipocte INT,
	tipo_apo INT,
	alergias VARCHAR(200) DEFAULT 'N/A',
	regimen_id INT,
	venc_cobertura DATE NOT NULL,
	tipo_empleado_id INT,
	eps_anterior_id INT,
	fecha_vinculacion_eps_anterior DATE NOT NULL,
	fondo_pension_id INT,
	discapacidad VARCHAR(200) NULL,
	email VARCHAR(120) NULL,
	arp_id INT,
	escolaridad_id INT,
	FOREIGN KEY (tipo_id) REFERENCES sis_tipo_documentos(id),
	FOREIGN KEY (tipo_usuario) REFERENCES sis_tipo_usuarios(id),
	FOREIGN KEY (cod_ciudad) REFERENCES ciudades(id),
	FOREIGN KEY (ocupacion_id) REFERENCES ocupaciones(id),
	FOREIGN KEY (est_afil_id) REFERENCES sis_estado_afiliacion(id),
	FOREIGN KEY (regimen_id) REFERENCES sis_regimen(id),
	FOREIGN KEY (tipo_empleado_id) REFERENCES sis_tipo_empleado(id),
	FOREIGN KEY (eps_anterior_id) REFERENCES sis_eps(id),
	FOREIGN KEY (fondo_pension_id) REFERENCES sis_fondo_pension(id),
	FOREIGN KEY (arp_id) REFERENCES sis_arp(id),    
	FOREIGN KEY (escolaridad_id) REFERENCES escolaridades(id),
	FOREIGN KEY (cod_usuario) REFERENCES sis_usuarios(id)
);

CREATE TABLE sis_medico (
	id int NOT NULL IDENTITY PRIMARY KEY,
	cedula BIGINT NOT NULL UNIQUE,
	nombre VARCHAR(200) NOT NULL,
	especialidad_id INT,
	registro BIGINT NOT NULL,
	tipo_id INT,
	tiempo INT NOT NULL,
	cod_usuario INT,
	es_medico TINYINT DEFAULT 1,
	es_anes TINYINT DEFAULT 0,
	es_ayu TINYINT DEFAULT 0,
	pago_prod DECIMAL (1,1) DEFAULT 0,
	valoresperado DECIMAL (1,1) DEFAULT 0,
	es_pediatra TINYINT DEFAULT 0,
	servicio_id INT,
	abre_historia TINYINT DEFAULT 1,
	cierra_historia TINYINT DEFAULT 1,
	es_auditor TINYINT DEFAULT 0,
	es_especialista TINYINT DEFAULT 0,
	estado TINYINT DEFAULT 0,
	tercero TINYINT DEFAULT 0,
	ApartaCita TINYINT DEFAULT 0,
	direccion VARCHAR(250) NOT NULL,
	telefono BIGINT NOT NULL,
	citaExterna TINYINT DEFAULT 0,
	leyendaConfirmarMedico VARCHAR(250) NULL,
	RequiereAuditoria TINYINT DEFAULT 0,
	NivelMctos INT DEFAULT 1,
	CodHistoriaPredeterminada INT NULL,
	EsMedicoFamiliar TINYINT DEFAULT 0,
	EsOdontologo TINYINT DEFAULT 0,
	EsPyp TINYINT DEFAULT 1,
	FOREIGN KEY (especialidad_id) REFERENCES sis_especialidades(id),
	FOREIGN KEY (tipo_id) REFERENCES sis_tipo_medico(id),
	FOREIGN KEY (cod_usuario) REFERENCES sis_usuarios(id),
	FOREIGN KEY (servicio_id) REFERENCES sis_servicios(id),
);

CREATE TABLE sis_asunto (
	id INT NOT NULL IDENTITY PRIMARY KEY,
	nombre VARCHAR(150) NOT NULL,
	id_oportunidad INT,
	tipo VARCHAR(200) NOT NULL,
	CitaOnline TINYINT DEFAULT 0,
	Especializada TINYINT DEFAULT 0,
	cierra_factura_confirmar_cita TINYINT DEFAULT 0,
	diagnostico VARCHAR(500) NOT NULL,
	defecto_cita_online TINYINT DEFAULT 0,
	es_terapia TINYINT DEFAULT 0,
	es_primer_vez TINYINT DEFAULT 0,
	es_pyp TINYINT DEFAULT 0,
	es_cita_grupal TINYINT DEFAULT 0
);
```

## nserción de registros
Algunas tablas ya deben tener datos por defecto para poder cruzar información, cómo especialidades, fondos_pension, etc… que son datos que dentro del sistema no van a cambiar

```sql
INSERT INTO sis_tipo_documentos (tipo_documento, descripcion) VALUES('CC', 'Cédula de Ciudadanía');
INSERT INTO sis_tipo_documentos (tipo_documento, descripcion) VALUES('TI', 'Tarjeta de Identidad');
INSERT INTO sis_tipo_documentos (tipo_documento, descripcion) VALUES('RC', 'Registro Civil');
INSERT INTO sis_tipo_documentos (tipo_documento, descripcion) VALUES('CE', 'Cédula de Extranjería');
INSERT INTO sis_tipo_documentos (tipo_documento, descripcion) VALUES('DNI', 'Documento Nacional de Identidad');
INSERT INTO sis_tipo_documentos (tipo_documento, descripcion) VALUES('PA', 'Pasaporte');
INSERT INTO sis_tipo_documentos (tipo_documento, descripcion) VALUES('NIT', 'Nit');

INSERT INTO sis_fondo_pension (fondo_pension) VALUES('Protección ');
INSERT INTO sis_fondo_pension (fondo_pension) VALUES('Porvenir');
INSERT INTO sis_fondo_pension (fondo_pension) VALUES('Colfondos');
INSERT INTO sis_fondo_pension (fondo_pension) VALUES('Colpensiones');
INSERT INTO sis_fondo_pension (fondo_pension) VALUES('Old mutual');

INSERT INTO sis_eps (entidad, codigo, nit) VALUES('COOSALUD EPS-S', 'ESS024 - EPS042', 900226715);
INSERT INTO sis_eps (entidad, codigo, nit) VALUES('NUEVA EPS', 'EPS037 - EPS041', 900156264);
INSERT INTO sis_eps (entidad, codigo, nit) VALUES('MUTUAL SER', 'ESS207 - EPS048', 806008394);
INSERT INTO sis_eps (entidad, codigo, nit) VALUES('ALIANSALUD EPS', 'EPS001', 830113831);
INSERT INTO sis_eps (entidad, codigo, nit) VALUES('SALUD TOTAL EPS S.A.', 'EPS002', 800130907);
INSERT INTO sis_eps (entidad, codigo, nit) VALUES('EPS SANITAS', 'EPS005', 800251440);
INSERT INTO sis_eps (entidad, codigo, nit) VALUES('EPS SURA', 'EPS010', 800088702);
INSERT INTO sis_eps (entidad, codigo, nit) VALUES('FAMISANAR EPS', 'EPS017', 830003564);
INSERT INTO sis_eps (entidad, codigo, nit) VALUES('SERVICIO OCCIDENTAL DE SALUD EPS SOS', 'EPS018', 805001157);
INSERT INTO sis_eps (entidad, codigo, nit) VALUES('SALUD MIA EPS', 'EPS046', 900914254);
INSERT INTO sis_eps (entidad, codigo, nit) VALUES('COMFENALCO VALLE', 'EPS012', 890303093);
INSERT INTO sis_eps (entidad, codigo, nit) VALUES('COMPENSAR EPS', 'EPS008', 860066942);
INSERT INTO sis_eps (entidad, codigo, nit) VALUES('EPM - EMPRESAS PUBLICAS DE MEDELLI', 'EAS016', 890904996);
INSERT INTO sis_eps (entidad, codigo, nit) VALUES('FONDO DE PASIVO SOCIAL DE FERROCARRILES NACIONALES DE COLOMBIA', 'EAS027', 800112806);
INSERT INTO sis_eps (entidad, codigo, nit) VALUES('CAJACOPI ATLANTICO CCF', 'CCF055', 890102044);
INSERT INTO sis_eps (entidad, codigo, nit) VALUES('CAPRESOCA EPS', 'EPS025', 891856000);
INSERT INTO sis_eps (entidad, codigo, nit) VALUES('COMFACHOCO CCF', 'CCF102', 891600091);
INSERT INTO sis_eps (entidad, codigo, nit) VALUES('COMFAORIENTE CCF', 'CCF050', 890500675);
INSERT INTO sis_eps (entidad, codigo, nit) VALUES('EPS FAMILIAR DE COLOMBIA CCF', 'CCF033', 901543761);
INSERT INTO sis_eps (entidad, codigo, nit) VALUES('ASMET SALUD', 'ESS062', 900935126);
INSERT INTO sis_eps (entidad, codigo, nit) VALUES('EMSSANAR E.S.S.', 'ESS118', 901021565);
INSERT INTO sis_eps (entidad, codigo, nit) VALUES('CAPITAL SALUD EPS-S', 'EPSS34', 900298372);
INSERT INTO sis_eps (entidad, codigo, nit) VALUES('SAVIA SALUD EPS', 'EPS40', 900604350);
INSERT INTO sis_eps (entidad, codigo, nit) VALUES('DUSAKAWI EPSI', 'EPSI01', 824001398);
INSERT INTO sis_eps (entidad, codigo, nit) VALUES('ASOCIACION INDIGENA DEL CAUCA EPSI', 'EPSI03', 817001773);
INSERT INTO sis_eps (entidad, codigo, nit) VALUES('ANAS WAYUU EPSI', 'EPSI04', 839000495);
INSERT INTO sis_eps (entidad, codigo, nit) VALUES('MALLAMAS EPSI', 'EPSI05', 837000084);
INSERT INTO sis_eps (entidad, codigo, nit) VALUES('PIJAOS SALUD EPSI', 'EPSI06', 809008362);
INSERT INTO sis_eps (entidad, codigo, nit) VALUES('SALUD BÓLIVAR EPS SAS', 'EPS047', 901438242);

INSERT INTO sis_estado_afiliacion (estado) VALUES('Afiliado Activo');
INSERT INTO sis_estado_afiliacion (estado) VALUES('Nuevo Afiliado');
INSERT INTO sis_estado_afiliacion (estado) VALUES('Afiliado Inactivo');
INSERT INTO sis_estado_afiliacion (estado) VALUES('Afiliado Pendiente');
INSERT INTO sis_estado_afiliacion (estado) VALUES('Beneficiario o Dependiente');

INSERT INTO sis_regimen (regimen, descripcion) VALUES('Régimen Contributivo', 'Régimen Contributivo de salud');
INSERT INTO sis_regimen (regimen, descripcion) VALUES('Régimen Subsidiado', 'Régimen Subsidiado de salud');

INSERT INTO sis_arp (arp) VALUES ('Positiva ARP');
INSERT INTO sis_arp (arp) VALUES ('Seguros Bolívar ARP');
INSERT INTO sis_arp (arp) VALUES ('Liberty Seguros ARP');
INSERT INTO sis_arp (arp) VALUES ('Sura ARP');
INSERT INTO sis_arp (arp) VALUES ('Colmena ARP');
INSERT INTO sis_arp (arp) VALUES ('Axa Colpatria ARP');
INSERT INTO sis_arp (arp) VALUES ('ARP Protección');
INSERT INTO sis_arp (arp) VALUES ('Mapfre Seguros ARP');
INSERT INTO sis_arp (arp) VALUES ('Seguros de Vida Suramericana ARP');
INSERT INTO sis_arp (arp) VALUES ('Seguros de Riesgos Laborales ARP (SRL ARP)');
INSERT INTO sis_arp (arp) VALUES ('ARP Seguros Generales');
INSERT INTO sis_arp (arp) VALUES ('ARP Seguros de Vida');
INSERT INTO sis_arp (arp) VALUES ('ARP Seguros del Estado');
INSERT INTO sis_arp (arp) VALUES ('ARP Seguros del Magisterio');
INSERT INTO sis_arp (arp) VALUES ('ARP Seguros del Banco de Bogotá');
INSERT INTO sis_arp (arp) VALUES ('ARP Seguros del Banco de Occidente');
INSERT INTO sis_arp (arp) VALUES ('ARP Seguros del Banco Popular');
INSERT INTO sis_arp (arp) VALUES ('ARP Seguros del Banco Caja Social');
INSERT INTO sis_arp (arp) VALUES ('ARP Seguros del Banco Davivienda');
INSERT INTO sis_arp (arp) VALUES ('ARP Seguros del Banco BBVA');
INSERT INTO sis_arp (arp) VALUES ('ARP Seguros de la Construcción');
INSERT INTO sis_arp (arp) VALUES ('ARP Seguros del Transporte');
INSERT INTO sis_arp (arp) VALUES ('ARP Seguros del Comercio');
INSERT INTO sis_arp (arp) VALUES ('ARP Seguros del Sector Agropecuario');
INSERT INTO sis_arp (arp) VALUES ('ARP Seguros de la Industria');
INSERT INTO sis_arp (arp) VALUES ('ARP Seguros de la Tecnología');
INSERT INTO sis_arp (arp) VALUES ('ARP Seguros de la Salud');
INSERT INTO sis_arp (arp) VALUES ('ARP Seguros del Servicio Público');
INSERT INTO sis_arp (arp) VALUES ('ARP Seguros del Servicio Doméstico');
INSERT INTO sis_arp (arp) VALUES ('ARP Seguros del Servicio Educativo');

INSERT INTO escolaridades (id, nivel_escolaridad) VALUES('Preescolar');
INSERT INTO escolaridades (id, nivel_escolaridad) VALUES('Educación Básica Primaria');
INSERT INTO escolaridades (id, nivel_escolaridad) VALUES('Educación Básica Secundaria');
INSERT INTO escolaridades (id, nivel_escolaridad) VALUES('Educación Media');
INSERT INTO escolaridades (id, nivel_escolaridad) VALUES('Educación Técnica y Tecnológica');
INSERT INTO escolaridades (id, nivel_escolaridad) VALUES('Educación Superior');

INSERT INTO ocupaciones (ocupacion) VALUES ('Médico');
INSERT INTO ocupaciones (ocupacion) VALUES ('Ingeniero');
INSERT INTO ocupaciones (ocupacion) VALUES ('Profesor');
INSERT INTO ocupaciones (ocupacion) VALUES ('Abogado');
INSERT INTO ocupaciones (ocupacion) VALUES ('Contador');
INSERT INTO ocupaciones (ocupacion) VALUES ('Arquitecto');
INSERT INTO ocupaciones (ocupacion) VALUES ('Administrador de Empresas');
INSERT INTO ocupaciones (ocupacion) VALUES ('Enfermero');
INSERT INTO ocupaciones (ocupacion) VALUES ('Programador');
INSERT INTO ocupaciones (ocupacion) VALUES ('Diseñador Gráfico');
INSERT INTO ocupaciones (ocupacion) VALUES ('Psicólogo');
INSERT INTO ocupaciones (ocupacion) VALUES ('Chef');
INSERT INTO ocupaciones (ocupacion) VALUES ('Electricista');
INSERT INTO ocupaciones (ocupacion) VALUES ('Carpintero');
INSERT INTO ocupaciones (ocupacion) VALUES ('Mecánico');
INSERT INTO ocupaciones (ocupacion) VALUES ('Plomero');
INSERT INTO ocupaciones (ocupacion) VALUES ('Fontanero');
INSERT INTO ocupaciones (ocupacion) VALUES ('Agricultor');
INSERT INTO ocupaciones (ocupacion) VALUES ('Economista');
INSERT INTO ocupaciones (ocupacion) VALUES ('Periodista');
INSERT INTO ocupaciones (ocupacion) VALUES ('Actor/Actriz');
INSERT INTO ocupaciones (ocupacion) VALUES ('Cantante');
INSERT INTO ocupaciones (ocupacion) VALUES ('Bailarín/Bailarina');
INSERT INTO ocupaciones (ocupacion) VALUES ('Policía');
INSERT INTO ocupaciones (ocupacion) VALUES ('Bombero');
INSERT INTO ocupaciones (ocupacion) VALUES ('Militar');
INSERT INTO ocupaciones (ocupacion) VALUES ('Piloto');
INSERT INTO ocupaciones (ocupacion) VALUES ('Marinero');
INSERT INTO ocupaciones (ocupacion) VALUES ('Taxista');
INSERT INTO ocupaciones (ocupacion) VALUES ('Conductor de autobús');
INSERT INTO ocupaciones (ocupacion) VALUES ('Secretario/Secretaria');
INSERT INTO ocupaciones (ocupacion) VALUES ('Recepcionista');
INSERT INTO ocupaciones (ocupacion) VALUES ('Asistente Administrativo');
INSERT INTO ocupaciones (ocupacion) VALUES ('Vendedor');
INSERT INTO ocupaciones (ocupacion) VALUES ('Gerente');
INSERT INTO ocupaciones (ocupacion) VALUES ('Director');
INSERT INTO ocupaciones (ocupacion) VALUES ('Estudiante');
INSERT INTO ocupaciones (ocupacion) VALUES ('Empresario');
INSERT INTO ocupaciones (ocupacion) VALUES ('Consultor');
INSERT INTO ocupaciones (ocupacion) VALUES ('Analista');
INSERT INTO ocupaciones (ocupacion) VALUES ('Investigador');
INSERT INTO ocupaciones (ocupacion) VALUES ('Artista');
INSERT INTO ocupaciones (ocupacion) VALUES ('Dentista');
INSERT INTO ocupaciones (ocupacion) VALUES ('Farmacéutico');
INSERT INTO ocupaciones (ocupacion) VALUES ('Terapeuta');
INSERT INTO ocupaciones (ocupacion) VALUES ('Entrenador');
INSERT INTO ocupaciones (ocupacion) VALUES ('Guardia de Seguridad');
INSERT INTO ocupaciones (ocupacion) VALUES ('Cajero');

INSERT INTO departamentos (departamento) VALUES ('Amazonas');
INSERT INTO departamentos (departamento) VALUES ('Antioquia');
INSERT INTO departamentos (departamento) VALUES ('Arauca');
INSERT INTO departamentos (departamento) VALUES ('Atlántico');
INSERT INTO departamentos (departamento) VALUES ('Bolívar');
INSERT INTO departamentos (departamento) VALUES ('Boyacá');
INSERT INTO departamentos (departamento) VALUES ('Caldas');
INSERT INTO departamentos (departamento) VALUES ('Caquetá');
INSERT INTO departamentos (departamento) VALUES ('Casanare');
INSERT INTO departamentos (departamento) VALUES ('Cauca');
INSERT INTO departamentos (departamento) VALUES ('Cesar');
INSERT INTO departamentos (departamento) VALUES ('Chocó');
INSERT INTO departamentos (departamento) VALUES ('Córdoba');
INSERT INTO departamentos (departamento) VALUES ('Cundinamarca');
INSERT INTO departamentos (departamento) VALUES ('Guainía');
INSERT INTO departamentos (departamento) VALUES ('Guaviare');
INSERT INTO departamentos (departamento) VALUES ('Huila');
INSERT INTO departamentos (departamento) VALUES ('La Guajira');
INSERT INTO departamentos (departamento) VALUES ('Magdalena');
INSERT INTO departamentos (departamento) VALUES ('Meta');
INSERT INTO departamentos (departamento) VALUES ('Nariño');
INSERT INTO departamentos (departamento) VALUES ('Norte de Santander');
INSERT INTO departamentos (departamento) VALUES ('Putumayo');
INSERT INTO departamentos (departamento) VALUES ('Quindío');
INSERT INTO departamentos (departamento) VALUES ('Risaralda');
INSERT INTO departamentos (departamento) VALUES ('San Andrés y Providencia');
INSERT INTO departamentos (departamento) VALUES ('Santander');
INSERT INTO departamentos (departamento) VALUES ('Sucre');
INSERT INTO departamentos (departamento) VALUES ('Tolima');
INSERT INTO departamentos (departamento) VALUES ('Valle del Cauca');
INSERT INTO departamentos (departamento) VALUES ('Vaupés');
INSERT INTO departamentos (departamento) VALUES ('Vichada');


INSERT INTO ciudades (ciudad, departamento_id) VALUES ('Leticia', 1);
INSERT INTO ciudades (ciudad, departamento_id) VALUES ('Medellín', 2);
INSERT INTO ciudades (ciudad, departamento_id) VALUES ('Envigado', 2);
INSERT INTO ciudades (ciudad, departamento_id) VALUES ('Bello', 2);
INSERT INTO ciudades (ciudad, departamento_id) VALUES ('Rionegro', 2);
INSERT INTO ciudades (ciudad, departamento_id) VALUES ('Itagüí', 2);
INSERT INTO ciudades (ciudad, departamento_id) VALUES ('Arauca', 3);
INSERT INTO ciudades (ciudad, departamento_id) VALUES ('Saravena', 3);
INSERT INTO ciudades (ciudad, departamento_id) VALUES ('Barranquilla', 4);
INSERT INTO ciudades (ciudad, departamento_id) VALUES ('Soledad', 4);
INSERT INTO ciudades (ciudad, departamento_id) VALUES ('Malambo', 4);
INSERT INTO ciudades (ciudad, departamento_id) VALUES ('Puerto Colombia', 4);
INSERT INTO ciudades (ciudad, departamento_id) VALUES ('Sabanagrande', 4);
INSERT INTO ciudades (ciudad, departamento_id) VALUES ('Cartagena', 5);
INSERT INTO ciudades (ciudad, departamento_id) VALUES ('Magangué', 5);
INSERT INTO ciudades (ciudad, departamento_id) VALUES ('Turbaco', 5);
INSERT INTO ciudades (ciudad, departamento_id) VALUES ('Arjona', 5);
INSERT INTO ciudades (ciudad, departamento_id) VALUES ('San Jacinto', 5);
INSERT INTO ciudades (ciudad, departamento_id) VALUES ('Tunja', 6);
INSERT INTO ciudades (ciudad, departamento_id) VALUES ('Duitama', 6);
INSERT INTO ciudades (ciudad, departamento_id) VALUES ('Sogamoso', 6);
INSERT INTO ciudades (ciudad, departamento_id) VALUES ('Chiquinquirá', 6);
INSERT INTO ciudades (ciudad, departamento_id) VALUES ('Puerto Boyacá', 6);
INSERT INTO ciudades (ciudad, departamento_id) VALUES ('Manizales', 7);
INSERT INTO ciudades (ciudad, departamento_id) VALUES ('La Dorada', 7);
INSERT INTO ciudades (ciudad, departamento_id) VALUES ('Chinchiná', 7);
INSERT INTO ciudades (ciudad, departamento_id) VALUES ('Anserma', 7);
INSERT INTO ciudades (ciudad, departamento_id) VALUES ('Villamaría', 7);
INSERT INTO ciudades (ciudad, departamento_id) VALUES ('Florencia', 8);
INSERT INTO ciudades (ciudad, departamento_id) VALUES ('San Vicente del Caguán', 8);
INSERT INTO ciudades (ciudad, departamento_id) VALUES ('Puerto Rico', 8);
INSERT INTO ciudades (ciudad, departamento_id) VALUES ('Belén de los Andaquíes', 8);
INSERT INTO ciudades (ciudad, departamento_id) VALUES ('Albania', 8);
INSERT INTO ciudades (ciudad, departamento_id) VALUES ('Yopal', 9);
INSERT INTO ciudades (ciudad, departamento_id) VALUES ('Aguazul', 9);
INSERT INTO ciudades (ciudad, departamento_id) VALUES ('Tauramena', 9);
INSERT INTO ciudades (ciudad, departamento_id) VALUES ('Villanueva', 9);
INSERT INTO ciudades (ciudad, departamento_id) VALUES ('Paz de Ariporo', 9);
INSERT INTO ciudades (ciudad, departamento_id) VALUES ('Popayán', 10);
INSERT INTO ciudades (ciudad, departamento_id) VALUES ('Santander de Quilichao', 10);
INSERT INTO ciudades (ciudad, departamento_id) VALUES ('Puerto Tejada', 10);
INSERT INTO ciudades (ciudad, departamento_id) VALUES ('Patía', 10);
INSERT INTO ciudades (ciudad, departamento_id) VALUES ('Cajibío', 10);
INSERT INTO ciudades (ciudad, departamento_id) VALUES ('Valledupar', 11);
INSERT INTO ciudades (ciudad, departamento_id) VALUES ('Aguachica', 11);
INSERT INTO ciudades (ciudad, departamento_id) VALUES ('Astillero', 11);
INSERT INTO ciudades (ciudad, departamento_id) VALUES ('San Diego', 11);
INSERT INTO ciudades (ciudad, departamento_id) VALUES ('La Paz', 11);
INSERT INTO ciudades (ciudad, departamento_id) VALUES ('Quibdó', 12);
INSERT INTO ciudades (ciudad, departamento_id) VALUES ('Tadó', 12);
INSERT INTO ciudades (ciudad, departamento_id) VALUES ('El Carmen de Atrato', 12);
INSERT INTO ciudades (ciudad, departamento_id) VALUES ('Condoto', 12);
INSERT INTO ciudades (ciudad, departamento_id) VALUES ('Riosucio', 12);
INSERT INTO ciudades (ciudad, departamento_id) VALUES ('Montería', 13);
INSERT INTO ciudades (ciudad, departamento_id) VALUES ('Sahagún', 13);
INSERT INTO ciudades (ciudad, departamento_id) VALUES ('Cereté', 13);
INSERT INTO ciudades (ciudad, departamento_id) VALUES ('Lorica', 13);
INSERT INTO ciudades (ciudad, departamento_id) VALUES ('Tierralta', 13);
INSERT INTO ciudades (ciudad, departamento_id) VALUES ('Bogotá', 14);
INSERT INTO ciudades (ciudad, departamento_id) VALUES ('Soacha', 14);
INSERT INTO ciudades (ciudad, departamento_id) VALUES ('Facatativá', 14);
INSERT INTO ciudades (ciudad, departamento_id) VALUES ('Zipaquirá', 14);
INSERT INTO ciudades (ciudad, departamento_id) VALUES ('Chía', 14);
INSERT INTO ciudades (ciudad, departamento_id) VALUES ('Inírida', 15);
INSERT INTO ciudades (ciudad, departamento_id) VALUES ('Barrancominas', 15);
INSERT INTO ciudades (ciudad, departamento_id) VALUES ('Cacahual', 15);
INSERT INTO ciudades (ciudad, departamento_id) VALUES ('La Guadalupe', 15);
INSERT INTO ciudades (ciudad, departamento_id) VALUES ('Mapiripana', 15);
INSERT INTO ciudades (ciudad, departamento_id) VALUES ('San José del Guaviare', 16);
INSERT INTO ciudades (ciudad, departamento_id) VALUES ('Calamar', 16);
INSERT INTO ciudades (ciudad, departamento_id) VALUES ('Miraflores', 16);
INSERT INTO ciudades (ciudad, departamento_id) VALUES ('El Retorno', 16);
INSERT INTO ciudades (ciudad, departamento_id) VALUES ('El Dorado', 16);
INSERT INTO ciudades (ciudad, departamento_id) VALUES ('Neiva', 17);
INSERT INTO ciudades (ciudad, departamento_id) VALUES ('Pitalito', 17);
INSERT INTO ciudades (ciudad, departamento_id) VALUES ('Garzón', 17);
INSERT INTO ciudades (ciudad, departamento_id) VALUES ('Campoalegre', 17);
INSERT INTO ciudades (ciudad, departamento_id) VALUES ('La Plata', 17);
INSERT INTO ciudades (ciudad, departamento_id) VALUES ('Riohacha', 18);
INSERT INTO ciudades (ciudad, departamento_id) VALUES ('Maicao', 18);
INSERT INTO ciudades (ciudad, departamento_id) VALUES ('Uribia', 18);
INSERT INTO ciudades (ciudad, departamento_id) VALUES ('Fonseca', 18);
INSERT INTO ciudades (ciudad, departamento_id) VALUES ('Manaure', 18);
INSERT INTO ciudades (ciudad, departamento_id) VALUES ('Santa Marta', 19);
INSERT INTO ciudades (ciudad, departamento_id) VALUES ('Ciénaga', 19);
INSERT INTO ciudades (ciudad, departamento_id) VALUES ('Fundación', 19);
INSERT INTO ciudades (ciudad, departamento_id) VALUES ('El Banco', 19);
INSERT INTO ciudades (ciudad, departamento_id) VALUES ('Aracataca', 19);
INSERT INTO ciudades (ciudad, departamento_id) VALUES ('Villavicencio', 20);
INSERT INTO ciudades (ciudad, departamento_id) VALUES ('Acacías', 20);
INSERT INTO ciudades (ciudad, departamento_id) VALUES ('Granada', 20);
INSERT INTO ciudades (ciudad, departamento_id) VALUES ('Puerto López', 20);
INSERT INTO ciudades (ciudad, departamento_id) VALUES ('Puerto Gaitán', 20);
INSERT INTO ciudades (ciudad, departamento_id) VALUES ('Pasto', 21);
INSERT INTO ciudades (ciudad, departamento_id) VALUES ('Tumaco', 21);
INSERT INTO ciudades (ciudad, departamento_id) VALUES ('Ipiales', 21);
INSERT INTO ciudades (ciudad, departamento_id) VALUES ('Túquerres', 21);
INSERT INTO ciudades (ciudad, departamento_id) VALUES ('La Unión', 21);
INSERT INTO ciudades (ciudad, departamento_id) VALUES ('Cúcuta', 22);
INSERT INTO ciudades (ciudad, departamento_id) VALUES ('Pamplona', 22);
INSERT INTO ciudades (ciudad, departamento_id) VALUES ('Ocaña', 22);
INSERT INTO ciudades (ciudad, departamento_id) VALUES ('Villa del Rosario', 22);
INSERT INTO ciudades (ciudad, departamento_id) VALUES ('Los Patios', 22);
INSERT INTO ciudades (ciudad, departamento_id) VALUES ('Mocoa', 23);
INSERT INTO ciudades (ciudad, departamento_id) VALUES ('Puerto Asís', 23);
INSERT INTO ciudades (ciudad, departamento_id) VALUES ('Orito', 23);
INSERT INTO ciudades (ciudad, departamento_id) VALUES ('Sibundoy', 23);
INSERT INTO ciudades (ciudad, departamento_id) VALUES ('Villagarzón', 23);
INSERT INTO ciudades (ciudad, departamento_id) VALUES ('Armenia', 24);
INSERT INTO ciudades (ciudad, departamento_id) VALUES ('Calarcá', 24);
INSERT INTO ciudades (ciudad, departamento_id) VALUES ('Montenegro', 24);
INSERT INTO ciudades (ciudad, departamento_id) VALUES ('Circasia', 24);
INSERT INTO ciudades (ciudad, departamento_id) VALUES ('La Tebaida', 24);
INSERT INTO ciudades (ciudad, departamento_id) VALUES ('Pereira', 25);
INSERT INTO ciudades (ciudad, departamento_id) VALUES ('Dosquebradas', 25);
INSERT INTO ciudades (ciudad, departamento_id) VALUES ('Santa Rosa de Cabal', 25);
INSERT INTO ciudades (ciudad, departamento_id) VALUES ('La Virginia', 25);
INSERT INTO ciudades (ciudad, departamento_id) VALUES ('Santuario', 25);
INSERT INTO ciudades (ciudad, departamento_id) VALUES ('San Andrés', 26);
INSERT INTO ciudades (ciudad, departamento_id) VALUES ('Bucaramanga', 27);
INSERT INTO ciudades (ciudad, departamento_id) VALUES ('Floridablanca', 27);
INSERT INTO ciudades (ciudad, departamento_id) VALUES ('Girón', 27);
INSERT INTO ciudades (ciudad, departamento_id) VALUES ('Piedecuesta', 27);
INSERT INTO ciudades (ciudad, departamento_id) VALUES ('Barrancabermeja', 27);
INSERT INTO ciudades (ciudad, departamento_id) VALUES ('Sincelejo', 28);
INSERT INTO ciudades (ciudad, departamento_id) VALUES ('Corozal', 28);
INSERT INTO ciudades (ciudad, departamento_id) VALUES ('Sampués', 28);
INSERT INTO ciudades (ciudad, departamento_id) VALUES ('San Marcos', 28);
INSERT INTO ciudades (ciudad, departamento_id) VALUES ('Morroa', 28);
INSERT INTO ciudades (ciudad, departamento_id) VALUES ('Ibagué', 29);
INSERT INTO ciudades (ciudad, departamento_id) VALUES ('Espinal', 29);
INSERT INTO ciudades (ciudad, departamento_id) VALUES ('Girardot', 29);
INSERT INTO ciudades (ciudad, departamento_id) VALUES ('Fresno', 29);
INSERT INTO ciudades (ciudad, departamento_id) VALUES ('Melgar', 29);
INSERT INTO ciudades (ciudad, departamento_id) VALUES ('Cali', 30);
INSERT INTO ciudades (ciudad, departamento_id) VALUES ('Buenaventura', 30);
INSERT INTO ciudades (ciudad, departamento_id) VALUES ('Palmira', 30);
INSERT INTO ciudades (ciudad, departamento_id) VALUES ('Buga', 30);
INSERT INTO ciudades (ciudad, departamento_id) VALUES ('Tuluá', 30);
INSERT INTO ciudades (ciudad, departamento_id) VALUES ('Mitú', 31);
INSERT INTO ciudades (ciudad, departamento_id) VALUES ('Puerto Carreño', 32);

INSERT INTO sis_especialidades (especialidad, codigo) VALUES ('Anestesiología', 'ANE01');
INSERT INTO sis_especialidades (especialidad, codigo) VALUES ('Cardiología', 'CAR02');
INSERT INTO sis_especialidades (especialidad, codigo) VALUES ('Dermatología', 'DER03');
INSERT INTO sis_especialidades (especialidad, codigo) VALUES ('Endocrinología', 'END04');
INSERT INTO sis_especialidades (especialidad, codigo) VALUES ('Gastroenterología', 'GAS05');
INSERT INTO sis_especialidades (especialidad, codigo) VALUES ('Geriatría', 'GER06');
INSERT INTO sis_especialidades (especialidad, codigo) VALUES ('Hematología', 'HEM07');
INSERT INTO sis_especialidades (especialidad, codigo) VALUES ('Infectología', 'INF08');
INSERT INTO sis_especialidades (especialidad, codigo) VALUES ('Medicina Familiar', 'MED09');
INSERT INTO sis_especialidades (especialidad, codigo) VALUES ('Medicina Física y Rehabilitación', 'MFR10');
INSERT INTO sis_especialidades (especialidad, codigo) VALUES ('Medicina Interna', 'MED11');
INSERT INTO sis_especialidades (especialidad, codigo) VALUES ('Nefrología', 'NEF12');
INSERT INTO sis_especialidades (especialidad, codigo) VALUES ('Neurología', 'NEU13');
INSERT INTO sis_especialidades (especialidad, codigo) VALUES ('Obstetricia y Ginecología', 'OBG14');
INSERT INTO sis_especialidades (especialidad, codigo) VALUES ('Oftalmología', 'OFT15');
INSERT INTO sis_especialidades (especialidad, codigo) VALUES ('Oncología', 'ONC16');
INSERT INTO sis_especialidades (especialidad, codigo) VALUES ('Ortopedia y Traumatología', 'ORT17');
INSERT INTO sis_especialidades (especialidad, codigo) VALUES ('Otorrinolaringología', 'OTO18');
INSERT INTO sis_especialidades (especialidad, codigo) VALUES ('Pediatría', 'PED19');
INSERT INTO sis_especialidades (especialidad, codigo) VALUES ('Psiquiatría', 'PSI20');
INSERT INTO sis_especialidades (especialidad, codigo) VALUES ('Radiología e Imagen', 'RAI21');
INSERT INTO sis_especialidades (especialidad, codigo) VALUES ('Reumatología', 'REU22');
INSERT INTO sis_especialidades (especialidad, codigo) VALUES ('Urología', 'URO23');
INSERT INTO sis_especialidades (especialidad, codigo) VALUES ('Medicina del Deporte', 'MDE24');
INSERT INTO sis_especialidades (especialidad, codigo) VALUES ('Medicina del Trabajo', 'MDT25');
INSERT INTO sis_especialidades (especialidad, codigo) VALUES ('Medicina de Emergencia', 'MDE26');
INSERT INTO sis_especialidades (especialidad, codigo) VALUES ('Medicina Forense', 'MFO27');
INSERT INTO sis_especialidades (especialidad, codigo) VALUES ('Medicina Intensiva', 'MIN28');
INSERT INTO sis_especialidades (especialidad, codigo) VALUES ('Medicina Nuclear', 'MNU29');
INSERT INTO sis_especialidades (especialidad, codigo) VALUES ('Medicina Preventiva y Salud Pública', 'MPS30');
INSERT INTO sis_especialidades (especialidad, codigo) VALUES ('Neumología', 'NEU31');
INSERT INTO sis_especialidades (especialidad, codigo) VALUES ('Anatomía Patológica', 'ANP32');
INSERT INTO sis_especialidades (especialidad, codigo) VALUES ('Cirugía General', 'CGE33');
INSERT INTO sis_especialidades (especialidad, codigo) VALUES ('Cirugía Pediátrica', 'CPD34');
INSERT INTO sis_especialidades (especialidad, codigo) VALUES ('Cirugía Plástica', 'CPL35');
INSERT INTO sis_especialidades (especialidad, codigo) VALUES ('Cirugía Torácica', 'CTO36');
INSERT INTO sis_especialidades (especialidad, codigo) VALUES ('Cirugía Vascular', 'CVS37');
INSERT INTO sis_especialidades (especialidad, codigo) VALUES ('Neurocirugía', 'NEC38');
INSERT INTO sis_especialidades (especialidad, codigo) VALUES ('Cirugía Oral y Maxilofacial', 'COM39');
INSERT INTO sis_especialidades (especialidad, codigo) VALUES ('Cirugía Cardiovascular', 'CCV40');
INSERT INTO sis_especialidades (especialidad, codigo) VALUES ('Cirugía Oncológica', 'CON41');
INSERT INTO sis_especialidades (especialidad, codigo) VALUES ('Psicología Clínica', 'PSC42');
INSERT INTO sis_especialidades (especialidad, codigo) VALUES ('Psicología Organizacional', 'PSO43');
INSERT INTO sis_especialidades (especialidad, codigo) VALUES ('Psicología Educativa', 'PSE44');
INSERT INTO sis_especialidades (especialidad, codigo) VALUES ('Psicología Forense', 'PSF45');
INSERT INTO sis_especialidades (especialidad, codigo) VALUES ('Psicología Social', 'PSS46');
INSERT INTO sis_especialidades (especialidad, codigo) VALUES ('Psicología Deportiva', 'PSD47');
INSERT INTO sis_especialidades (especialidad, codigo) VALUES ('Psicología Clínica Infantil', 'PCI48');
INSERT INTO sis_especialidades (especialidad, codigo) VALUES ('Psicología de la Salud', 'PSS49');
INSERT INTO sis_especialidades (especialidad, codigo) VALUES ('Psicología Gerontológica', 'PSG50');
```

## Consultas

