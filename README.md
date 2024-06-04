# tallerSQL

## Diagrama ER
Este es el diagrama que se propone para la realización del ejercicio

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

Aqui puedes copiar el script para crear la estructura de la base de datos, es decir, todas las tablas con sus respectivas relaciones, una vez ejecutado estas sentencias, el resultado de nuestras tablas será el siguiente 

![ER](https://github.com/10075016-22/tallerSQL/assets/11299320/ae869698-4dee-4270-a268-59bc257002f1)


Si!, un poco desordenado, pero es algo :) 

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
	pass varchar(250) NOT NULL,
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

CREATE TABLE sis_codigo_diagnostico (
	id int NOT NULL IDENTITY PRIMARY KEY,
	codigo varchar(150) NOT NULL,
	descripcion varchar(1500) NOT NULL
);

CREATE TABLE sis_estados_cita (
	id int NOT NULL IDENTITY PRIMARY KEY,
	estado varchar(150) NOT NULL
);

CREATE TABLE sis_tipo_paciente (
	id int NOT NULL IDENTITY PRIMARY KEY,
	tipo varchar(150) NOT NULL,
	descripcion varchar(1500) NOT NULL,
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

CREATE TABLE sis_formatos (
	id INT NOT NULL IDENTITY PRIMARY KEY,
    codigo VARCHAR(50),
    descripcion VARCHAR(255)
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

CREATE TABLE sis_historia_clinica (
	id int NOT NULL IDENTITY PRIMARY KEY,
	estudio TEXT NOT NULL,
	ingreso DATETIME NOT NULL,
	tipo_id_paciente INT,
	id_paciente INT,
	codigo_formato INT,
    grupo VARCHAR(50),
    campo VARCHAR(255),
    valor_campo VARCHAR(MAX),
    ref_valor_campo VARCHAR(MAX),
    codigo_diagnostico INT,
    fecha_ingreso DATE,
    hora_ingreso TIME,
    fecha_atencion DATE,
    hora_atencion TIME,
    fecha_salida DATE,
    hora_salida TIME,
	FOREIGN KEY (tipo_id_paciente) REFERENCES sis_tipo_paciente(id),
	FOREIGN KEY (id_paciente) REFERENCES sis_paciente(id),
	FOREIGN KEY (codigo_diagnostico ) REFERENCES sis_codigo_diagnostico(id),
	FOREIGN KEY (codigo_formato) REFERENCES sis_formatos(id)

);

CREATE TABLE sis_citas (
    id int NOT NULL IDENTITY PRIMARY KEY,
    cod_medi INT,
    fecha_usuario_desea_cita DATE,
    fecha DATE,
    hora TIME,
    meridiano VARCHAR(50),
    estado INT,
    asunto INT,
    observacion VARCHAR(MAX),
    estudio VARCHAR(255),
    fecha_solicitud DATE,
    motivo VARCHAR(MAX),
    id_empresa_cita INT,
    hora_cancela TIME NULL,
    copago DECIMAL(10, 2),
    pagado DECIMAL(10, 2),
    idconfirmo INT,
    cajero VARCHAR(255),
    pyp VARCHAR(255),
    cod_user_asigna_cita INT,
    tipocita VARCHAR(50),
    id_especialidad INT,
    id_procedimiento_realizar INT,
    id_usuario_aplaza INT NULL,
    motivo_aplaza VARCHAR(MAX),
    fecha_aplaza DATE,
    contrato VARCHAR(255),
    tipo_servicio_id INT,
    sede VARCHAR(250),
    id_stock INT,
    motivo_cancela VARCHAR(MAX),
    id_usuario_cancela INT,
    primera_vez_control TINYINT DEFAULT 0,
    fecha_confirmacion DATE,
    hora_confirmacion TIME,
    formaSolicitud VARCHAR(255),
    id_programacion INT,
    citaHC INT,
    motivo_incumple VARCHAR(MAX),
    id_usuario_incumple INT NULL,
    lugarAtencion VARCHAR(255),
    btnMarcarAtendida VARCHAR(255),
    usuarioMarcaAtendida VARCHAR(255),
    Adicional VARCHAR(MAX),
    CodGrupo VARCHAR(50),
    txtObservacionGrupo VARCHAR(MAX),
    EsCitaMultiple TINYINT DEFAULT 0,
    id_cama INT,
    tipo_cama VARCHAR(50),
    ActividadServicio VARCHAR(255),
    ActividadAsunto VARCHAR(255),
    Modificada TINYINT DEFAULT 0,
    DescuentoAutorizado DECIMAL(10, 2),
    PermiteDevolucion TINYINT DEFAULT 0,
    UsuarioAutorizaDsctoYDevo VARCHAR(255),
    GeneroHCAlConfirmar TINYINT DEFAULT 1,
    NumeroPoliza VARCHAR(255),
    CodMedTratante VARCHAR(50),
    id_documento VARCHAR(50),
    IdPcteTratamiento INT,
    IdActividadTratamiento INT,
    ConsecutivoZI_Tratamiento VARCHAR(50),
    EmailEnviado TINYINT DEFAULT 1,
    TipoDescuento VARCHAR(255),
    AsistenciaConfirmada TINYINT DEFAULT 1,
    IdTipoConfirmacionAsistencia INT,
    IdUsuarioConfirmaAsistencia INT,
    FechaConfirmaAsistencia DATE,
    ObservacionConfirmaAsistencia VARCHAR(MAX),
    FechaSistemaConfirmaAsistencia DATETIME,
    UsuarioRevierteConfirmaAsistencia VARCHAR(255),
    ObservacionRevierteConfirmaAsistencia VARCHAR(MAX),
    FechaSistemaRevierteConfirmaAsistencia DATETIME,
    acompanante VARCHAR(255),
    telefono_acompanante VARCHAR(50),

	FOREIGN KEY (cod_medi) REFERENCES sis_medico(id),
	FOREIGN KEY (id_empresa_cita) REFERENCES sis_eps(id),
	FOREIGN KEY (estado) REFERENCES sis_estados_cita(id),
	FOREIGN KEY (cod_user_asigna_cita) REFERENCES sis_usuarios(id),
	FOREIGN KEY (id_especialidad) REFERENCES sis_especialidades(id),
	FOREIGN KEY (tipo_servicio_id) REFERENCES sis_servicios(id),
	FOREIGN KEY (citaHC) REFERENCES sis_historia_clinica(id),
	FOREIGN KEY (asunto) REFERENCES sis_asunto(id)
);
```

## Inserción de registros
Algunas tablas ya deben tener datos por defecto para poder cruzar información, cómo especialidades, fondos_pension, etc… que son datos que dentro del sistema no van a cambiar

- Tipos de documentos
```sql
INSERT INTO sis_tipo_documentos (tipo_documento, descripcion) VALUES('CC', 'Cédula de Ciudadanía');
INSERT INTO sis_tipo_documentos (tipo_documento, descripcion) VALUES('TI', 'Tarjeta de Identidad');
INSERT INTO sis_tipo_documentos (tipo_documento, descripcion) VALUES('RC', 'Registro Civil');
INSERT INTO sis_tipo_documentos (tipo_documento, descripcion) VALUES('CE', 'Cédula de Extranjería');
INSERT INTO sis_tipo_documentos (tipo_documento, descripcion) VALUES('DNI', 'Documento Nacional de Identidad');
INSERT INTO sis_tipo_documentos (tipo_documento, descripcion) VALUES('PA', 'Pasaporte');
INSERT INTO sis_tipo_documentos (tipo_documento, descripcion) VALUES('NIT', 'Nit');
```

- Fondos de pensión
```sql
INSERT INTO sis_fondo_pension (fondo_pension) VALUES('Protección ');
INSERT INTO sis_fondo_pension (fondo_pension) VALUES('Porvenir');
INSERT INTO sis_fondo_pension (fondo_pension) VALUES('Colfondos');
INSERT INTO sis_fondo_pension (fondo_pension) VALUES('Colpensiones');
INSERT INTO sis_fondo_pension (fondo_pension) VALUES('Old mutual');
```

-  Eps
```sql
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
```

-  Estados de afiliación
```sql
INSERT INTO sis_estado_afiliacion (estado) VALUES('Afiliado Activo');
INSERT INTO sis_estado_afiliacion (estado) VALUES('Nuevo Afiliado');
INSERT INTO sis_estado_afiliacion (estado) VALUES('Afiliado Inactivo');
INSERT INTO sis_estado_afiliacion (estado) VALUES('Afiliado Pendiente');
INSERT INTO sis_estado_afiliacion (estado) VALUES('Beneficiario o Dependiente');
```

-  Regimen
```sql
INSERT INTO sis_regimen (regimen, descripcion) VALUES('Régimen Contributivo', 'Régimen Contributivo de salud');
INSERT INTO sis_regimen (regimen, descripcion) VALUES('Régimen Subsidiado', 'Régimen Subsidiado de salud');
```

-  ARP
```sql
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
```

-  Nivel de escolaridad
```sql
INSERT INTO escolaridades (nivel_escolaridad) VALUES('Preescolar');
INSERT INTO escolaridades (nivel_escolaridad) VALUES('Educación Básica Primaria');
INSERT INTO escolaridades (nivel_escolaridad) VALUES('Educación Básica Secundaria');
INSERT INTO escolaridades (nivel_escolaridad) VALUES('Educación Media');
INSERT INTO escolaridades (nivel_escolaridad) VALUES('Educación Técnica y Tecnológica');
INSERT INTO escolaridades (nivel_escolaridad) VALUES('Educación Superior');
```

-  Ocupaciones
```sql
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
```

-  Departamentos
```sql
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
```

-  Ciudades
```sql
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
```

-  Especialidades
```sql
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

-  Servicios
```sql
INSERT INTO sis_servicios (servicio) VALUES ('Consulta General');
INSERT INTO sis_servicios (servicio) VALUES ('Pediatría');
INSERT INTO sis_servicios (servicio) VALUES ('Ginecología');
INSERT INTO sis_servicios (servicio) VALUES ('Cardiología');
INSERT INTO sis_servicios (servicio) VALUES ('Dermatología');
INSERT INTO sis_servicios (servicio) VALUES ('Neurología');
INSERT INTO sis_servicios (servicio) VALUES ('Traumatología');
INSERT INTO sis_servicios (servicio) VALUES ('Oftalmología');
INSERT INTO sis_servicios (servicio) VALUES ('Otorrinolaringología');
INSERT INTO sis_servicios (servicio) VALUES ('Medicina Interna');
INSERT INTO sis_servicios (servicio) VALUES ('Radiología');
INSERT INTO sis_servicios (servicio) VALUES ('Cirugía General');
INSERT INTO sis_servicios (servicio) VALUES ('Psiquiatría');
INSERT INTO sis_servicios (servicio) VALUES ('Nutrición');
INSERT INTO sis_servicios (servicio) VALUES ('Odontología');
```

-  Tipo de médico
```sql
INSERT INTO sis_tipo_medico (tipo) VALUES ('Médico General');
INSERT INTO sis_tipo_medico (tipo) VALUES ('Médico Especialista');
INSERT INTO sis_tipo_medico (tipo) VALUES ('Médico Internista');
INSERT INTO sis_tipo_medico (tipo) VALUES ('Médico Pediatra');
INSERT INTO sis_tipo_medico (tipo) VALUES ('Médico Ginecólogo');
INSERT INTO sis_tipo_medico (tipo) VALUES ('Médico Cirujano');
INSERT INTO sis_tipo_medico (tipo) VALUES ('Médico Anestesiólogo');
INSERT INTO sis_tipo_medico (tipo) VALUES ('Médico Cardiólogo');
INSERT INTO sis_tipo_medico (tipo) VALUES ('Médico Dermatólogo');
INSERT INTO sis_tipo_medico (tipo) VALUES ('Médico Oftalmólogo');
INSERT INTO sis_tipo_medico (tipo) VALUES ('Médico Otorrinolaringólogo');
INSERT INTO sis_tipo_medico (tipo) VALUES ('Médico Psiquiatra');
INSERT INTO sis_tipo_medico (tipo) VALUES ('Médico Traumatólogo');
INSERT INTO sis_tipo_medico (tipo) VALUES ('Médico Radiólogo');
INSERT INTO sis_tipo_medico (tipo) VALUES ('Médico Oncólogo');
```

-  Tipos de usuario
```sql
INSERT INTO sis_tipo_usuarios (tipo_usuario) VALUES ('SuperAdmin');
INSERT INTO sis_tipo_usuarios (tipo_usuario) VALUES ('Administrador');
INSERT INTO sis_tipo_usuarios (tipo_usuario) VALUES ('Médico');
INSERT INTO sis_tipo_usuarios (tipo_usuario) VALUES ('Secretaria');
INSERT INTO sis_tipo_usuarios (tipo_usuario) VALUES ('Auxiliar');
INSERT INTO sis_tipo_usuarios (tipo_usuario) VALUES ('Prácticante');
INSERT INTO sis_tipo_usuarios (tipo_usuario) VALUES ('Contador');
INSERT INTO sis_tipo_usuarios (tipo_usuario) VALUES ('Paramédico');
INSERT INTO sis_tipo_usuarios (tipo_usuario) VALUES ('Vigilante');
INSERT INTO sis_tipo_usuarios (tipo_usuario) VALUES ('Paciente');
```

-  Estado de cita
```sql
INSERT INTO sis_estados_cita (estado) VALUES('Atendida');
INSERT INTO sis_estados_cita (estado) VALUES('Cancelada');
INSERT INTO sis_estados_cita (estado) VALUES('Completada');
INSERT INTO sis_estados_cita (estado) VALUES('Incumplida');
```

-  Códigos de diagnosticos
```sql
INSERT INTO sis_codigo_diagnostico (codigo, descripcion) VALUES 
('D460', 'ANEMIA REFRACTARIA SIN SIDEROBLASTOS, ASI DESCRITA'),
('D51', 'ANEMIA POR DEFICIENCIA DE VITAMINA B12'),
('D52', 'ANEMIA POR DEFICIENCIA DE FOLATOS'),
('D53', 'OTRAS ANEMIAS NUTRICIONALES'),
('D55', 'ANEMIA DEBIDA A TRASTORNOS ENZIMATICOS'),
('D570', 'ANEMIA FALCIFORME CON CRISIS'),
('D58', 'OTRAS ANEMIAS HEMOLITICAS HEREDITARIAS'),
('D59', 'ANEMIA HEMOLITICA ADQUIRIDA'),
('D61', 'OTRAS ANEMIAS APLASTICAS'),
('D62', 'ANEMIA POSTHEMORRAGICA AGUDA'),
('D63', 'ANEMIA EN ENFERMEDADES CRONICAS CLASIFICADAS EN OTRA PARTE'),
('D64', 'OTRAS ANEMIAS'),
('O990', 'ANEMIA QUE COMPLICA EL EMBARAZO, EL PARTO Y EL PUERPERIO'),
('I253', 'ANEURISMA CARDIACO'),
('I281', 'ANEURISMA DE LA ARTERIA PULMONAR'),
('I671', 'ANEURISMA CEREBRAL, SIN RUPTURA'),
('I71', 'ANEURISMA Y DISECCION AORTICOS'),
('I72', 'OTROS ANEURISMAS'),
('I49', 'OTRAS ARRITMIAS CARDIACAS'),
('I498', 'OTRAS ARRITMIAS CARDIACAS ESPECIFICADAS'),
('M058', 'OTRAS ARTRITIS REUMATOIDEAS SEROPOSITIVAS'),
('M059', 'ARTRITIS REUMATOIDEA SEROPOSITIVA, SIN OTRA ESPECIFICACION'),
('M124', 'HIDRARTROSIS INTERMITENTE'),
('M15', 'POLIARTROSIS'),
('M158', 'OTRAS POLIARTROSIS'),
('M16', 'COXARTROSIS [ARTROSIS DE LA CADERA]'),
('M17', 'GONARTROSIS [ARTROSIS DE LA RODILLA]'),
('M179', 'GONARTROSIS, NO ESPECIFICADA'),
('M18', 'ARTROSIS DE LA PRIMERA ARTICULACION CARPOMETACARPIANA'),
('M19', 'OTRAS ARTROSIS'),
('M250', 'HEMARTROSIS'),
('M841', 'FALTA DE CONSOLIDACION DE FRACTURA [SEUDOARTROSIS]'),
('M960', 'SEUDOARTROSIS CONSECUTIVA A FUSION O ARTRODESIS'),
('G933', 'SINDROME DE FATIGA POSTVIRAL'),
('M484', 'FRACTURA DE VERTEBRA POR FATIGA'),
('R53', 'MALESTAR Y FATIGA'),
('T676', 'FATIGA POR CALOR, TRANSITORIA'),
('E10', 'DIABETES MELLITUS INSULINODEPENDIENTE'),
('E107', 'DIABETES MELLITUS INSULINODEPENDIENTE, CON COMPLICACIONES MULTIPLES'),
('E108', 'DIABETES MELLITUS INSULINODEPENDIENTE, CON COMPLICACIONES NO ESPECIFICADAS'),
('E11', 'DIABETES MELLITUS NO INSULINODEPENDIENTE'),
('E117', 'DIABETES MELLITUS NO INSULINODEPENDIENTE, CON COMPLICACIONES MULTIPLES'),
('E118', 'DIABETES MELLITUS NO INSULINODEPENDIENTE, CON COMPLICACIONES NO ESPECIFICAD'),
('E12', 'DIABETES MELLITUS ASOCIADA CON DESNUTRICION'),
('E13', 'OTRAS DIABETES MELLITUS ESPECIFICADAS'),
('E14', 'DIABETES MELLITUS, NO ESPECIFICADA'),
('E232', 'DIABETES INSIPIDA'),
('O240', 'DIABETES MELLITUS PREEXISTENTE INSULINODEPENDIENTE, EN EL EMBARAZO'),
('O241', 'DIABETES MELLITUS PREEXISTENTE NO INSULINODEPENDIENTE, EN EL EMBARAZO'),
('P700', 'SINDROME DEL RECIEN NACIDO DE MADRE CON DIABETES GESTACIONAL'),
('Z131', 'EXAMEN DE PESQUISA ESPECIAL PARA DIABETES MELLITUS'),
('Z833', 'HISTORIA FAMILIAR DE DIABETES MELLITUS'),
('A09', 'DIARREA Y GASTROENTERITIS DE PRESUNTO ORIGEN INFECCIOSO'),
('K580', 'SINDROME DEL COLON IRRITABLE CON DIARREA'),
('K591', 'DIARREA FUNCIONAL'),
('P783', 'DIARREA NEONATAL NO INFECCIOSA'),
('C81', 'ENFERMEDAD DE HODGKIN'),
('B212', 'ENFERMEDAD POR VIH, RESULTANTE EN OTROS TIPOS DE LINFOMA NO HODGKIN'),
('C817', 'OTROS TIPOS DE ENFERMEDAD DE HODGKIN'),
('C819', 'ENFERMEDAD DE HODGKIN, NO ESPECIFICADA'),
('C82', 'LINFOMA NO HODGKIN FOLICULAR [NODULAR]'),
('C83', 'LINFOMA NO HODGKIN DIFUSO'),
('C85', 'LINFOMA NO HODGKIN DE OTRO TIPO Y EL NO ESPECIFICADO'),
('B86', 'ESCABIOSIS'),
('A545', 'FARINGITIS GONOCOCICA'),
('B085', 'FARINGITIS VESICULAR ENTEROVIRICA'),
('J00', 'RINOFARINGITIS AGUDA [RESFRIADO COMUN]'),
('J02', 'FARINGITIS AGUDA'),
('J020', 'FARINGITIS ESTREPTOCOCICA'),
('J060', 'LARINGOFARINGITIS AGUDA'),
('J31', 'RINITIS, RINOFARINGITIS Y FARINGITIS CRONICAS'),
('J312', 'FARINGITIS CRONICA'),
('E84', 'FIBROSIS QUISTICA'),
('E840', 'FIBROSIS QUISTICA CON MANIFESTACIONES PULMONARES'),
('E841', 'FIBROSIS QUISTICA CON MANIFESTACIONES INTESTINALES'),
('A68', 'FIEBRES RECURRENTES'),
('A78', 'FIEBRE Q'),
('R50', 'FIEBRE DE ORIGEN DESCONOCIDO'),
('R500', 'FIEBRE CON ESCALOFRIO'),
('R501', 'FIEBRE PERSISTENTE'),
('A01', 'FIEBRES TIFOIDEA Y PARATIFOIDEA'),
('A93', 'OTRAS FIEBRES VIRALES TRANSMITIDAS POR ARTROPODOS, NO CLASIFICADAS EN OTRA'),
('A95', 'FIEBRE AMARILLA'),
('A960', 'FIEBRE HEMORRAGICA DE JUNIN'),
('I00', 'FIEBRE REUMATICA SIN MENCION DE COMPLICACION CARDIACA'),
('I01', 'FIEBRE REUMATICA CON COMPLICACION CARDIACA'),
('L540', 'ERITEMA MARGINADO EN LA FIEBRE REUMATICA AGUDA (I00+)'),
('A09', 'DIARREA Y GASTROENTERITIS DE PRESUNTO ORIGEN INFECCIOSO'),
('K52', 'OTRAS COLITIS Y GASTROENTERITIS NO INFECCIOSAS'),
('K520', 'COLITIS Y GASTROENTERITIS DEBIDAS A RADIACION'),
('K521', 'COLITIS Y GASTROENTERITIS TOXICAS'),
('K522', 'COLITIS Y GASTROENTERITIS ALERGICAS Y DIETETICAS'),
('K529', 'COLITIS Y GASTROENTERITIS NO INFECCIOSAS, NO ESPECIFICADAS'),
('K50', 'ENFERMEDAD DE CROHN [ENTERITIS REGIONAL]'),
('A083', 'OTRAS ENTERITIS VIRALES'),
('R31', 'HEMATURIA, NO ESPECIFICADA'),
('N02', 'HEMATURIA RECURRENTE Y PERSISTENTE'),
('B15', 'HEPATITIS AGUDA TIPO A'),
('B16', 'HEPATITIS AGUDA TIPO B'),
('B17', 'OTRAS HEPATITIS VIRALES AGUDAS'),
('B171', 'HEPATITIS AGUDA TIPO C'),
('B172', 'HEPATITIS AGUDA TIPO E'),
('B18', 'HEPATITIS VIRAL CRONICA'),
('B19', 'HEPATITIS VIRAL, SIN OTRA ESPECIFICACION'),
('B942', 'SECUELAS DE HEPATITIS VIRAL'),
('K701', 'HEPATITIS ALCOHOLICA'),
('K712', 'ENFERMEDAD TOXICA DEL HIGADO CON HEPATITIS AGUDA'),
('K713', 'ENFERMEDAD TOXICA DEL HIGADO CON HEPATITIS CRONICA PERSISTENTE'),
('K73', 'HEPATITIS CRONICA, NO CLASIFICADA EN OTRA PARTE'),
('K752', 'HEPATITIS REACTIVA NO ESPECIFICA'),
('O984', 'HEPATITIS VIRAL QUE COMPLICA EL EMBARAZO, EL PARTO Y EL PUERPERIO'),
('P353', 'HEPATITIS VIRAL CONGENITA'),
('Z205', 'CONTACTO CON Y EXPOSICION A HEPATITIS VIRAL'),
('Z225', 'PORTADOR DE HEPATITIS VIRAL'),
('Z246', 'NECESIDAD DE INMUNIZACION CONTRA LA HEPATITIS VIRAL'),
('A60', 'INFECCION ANOGENITAL DEBIDA A VIRUS DEL HERPES [HERPES SIMPLE]'),
('B00', 'INFECCIONES HERPETICAS [HERPES SIMPLE]'),
('B02', 'HERPES ZOSTER'),
('B028', 'HERPES ZOSTER CON OTRAS COMPLICACIONES'),
('B029', 'HERPES ZOSTER SIN COMPLICACIONES'),
('B270', 'MONONUCLEOSIS DEBIDA A HERPES VIRUS GAMMA'),
('G530', 'NEURALGIA POSTHERPES ZOSTER (B02.2+)'),
('H191', 'QUERATITIS Y QUERATOCONJUNTIVITIS POR HERPES SIMPLE (B00.5+)'),
('O264', 'HERPES GESTACIONAL'),
('P352', 'INFECCIONES CONGENITAS POR VIRUS DEL HERPES SIMPLE'),
('I10', 'HIPERTENSION ESENCIAL (PRIMARIA)'),
('I15', 'HIPERTENSION SECUNDARIA'),
('I270', 'HIPERTENSION PULMONAR PRIMARIA'),
('K766', 'HIPERTENSION PORTAL'),
('O10', 'HIPERTENSION PREEXISTENTE QUE COMPLICA EL EMBARAZO, EL PARTO Y EL PUERPERIO'),
('O16', 'HIPERTENSION MATERNA, NO ESPECIFICADA'),
('P292', 'HIPERTENSION NEONATAL'),
('R030', 'LECTURA ELEVADA DE LA PRESION SANGUINEA, SIN DIAGNOSTICO DE HIPERTENSION'),
('E05', 'TIROTOXICOSIS [HIPERTIROIDISMO]'),
('P721', 'HIPERTIROIDISMO NEONATAL TRANSITORIO'),
('E02', 'HIPOTIROIDISMO SUBCLINICO POR DEFICIENCIA DE YODO'),
('E03', 'OTRO HIPOTIROIDISMO'),
('N17', 'INSUFICIENCIA RENAL AGUDA'),
('N18', 'INSUFICIENCIA RENAL CRONICA'),
('N19', 'INSUFICIENCIA RENAL NO ESPECIFICADA'),
('O084', 'INSUFICIENCIA RENAL CONSECUTIVA AL ABORTO, AL EMBARAZO ECTOPICO Y AL EMBARA'),
('O904', 'INSUFICIENCIA RENAL AGUDA POSTPARTO'),
('P960', 'INSUFICIENCIA RENAL CONGENITA'),
('C85', 'LINFOMA NO HODGKIN DE OTRO TIPO Y EL NO ESPECIFICADO'),
('C83', 'LINFOMA NO HODGKIN DIFUSO'),
('C82', 'LINFOMA NO HODGKIN FOLICULAR [NODULAR]'),
('C84', 'LINFOMA DE CELULAS T, PERIFERICO Y CUTANEO'),
('L412', 'PAPULOSIS LINFOMATOIDE'),
('H811', 'VERTIGO PAROXISTICO BENIGNO'),
('C43', 'MELANOMA MALIGNO DE LA PIEL'),
('D03', 'MELANOMA IN SITU'),
('C900', 'MIELOMA MULTIPLE'),
('M820', 'OSTEOPOROSIS EN MIELOMATOSIS MULTIPLE (C90.0+)'),
('B27', 'MONONUCLEOSIS INFECCIOSA'),
('B270', 'MONONUCLEOSIS DEBIDA A HERPES VIRUS GAMMA'),
('B271', 'MONONUCLEOSIS POR CITOMEGALOVIRUS'),
('E66', 'OBESIDAD'),
('B26', 'PAROTIDITIS INFECCIOSA'),
('B268', 'PAROTIDITIS INFECCIOSA CON OTRAS COMPLICACIONES'),
('B269', 'PAROTIDITIS, SIN COMPLICACIONES'),
('Z250', 'NECESIDAD DE INMUNIZACION SOLO CONTRA LA PAROTIDITIS'),
('M25', 'OTROS TRASTORNOS ARTICULARES, NO CLASIFICADOS EN OTRA PARTE'),
('M245', 'CONTRACTURA ARTICULAR'),
('M253', 'OTRAS INESTABILIDADES ARTICULARES'),
('M259', 'TRASTORNO ARTICULAR, NO ESPECIFICADO'),
('C46', 'SARCOMA DE KAPOSI'),
('C850', 'LINFOSARCOMA'),
('C923', 'SARCOMA MIELOIDE'),
('J01', 'SINUSITIS AGUDA'),
('J32', 'SINUSITIS CRONICA'),
('R630', 'ANOREXIA'),
('G40', 'EPILEPSIA'),
('F803', 'AFASIA ADQUIRIDA CON EPILEPSIA [LANDAU-KLEFFNER]'),
('Z820', 'HISTORIA FAMILIAR DE EPILEPSIA Y OTRAS ENFERMEDADES DEL SISTEMA NERVIOSO'),
('I50', 'INSUFICIENCIA CARDIACA'),
('P290', 'INSUFICIENCIA CARDIACA NEONATAL'),
('J00', 'RINOFARINGITIS AGUDA [RESFRIADO COMUN]'),
('J311', 'RINOFARINGITIS CRONICA'),
('J03', 'AMIGDALITIS AGUDA'),
('J350', 'AMIGDALITIS CRONICA'),
('J80', 'SINDROME DE DIFICULTAD RESPIRATORIA DEL ADULTO'),
('J96', 'INSUFICIENCIA RESPIRATORIA, NO CLASIFICADA EN OTRA PARTE'),
('T17', 'CUERPO EXTRANIO EN LAS VIAS RESPIRATORIAS'),
('J30', 'RINITIS ALERGICA Y VASOMOTORA'),
('J31', 'RINITIS, RINOFARINGITIS Y FARINGITIS CRONICAS'),
('J310', 'RINITIS CRONICA'),
('J45', 'ASMA'),
('J450', 'ASMA PREDOMINANTEMENTE ALERGICA'),
('J451', 'ASMA NO ALERGICA'),
('K25', 'ULCERA GASTRICA'),
('K26', 'ULCERA DUODENAL'),
('K27', 'ULCERA PEPTICA, DE SITIO NO ESPECIFICADO'),
('K28', 'ULCERA GASTROYEYUNAL'),
('K29', 'GASTRITIS Y DUODENITIS'),
('K291', 'OTRAS GASTRITIS AGUDAS'),
('K295', 'GASTRITIS CRONICA, NO ESPECIFICADA'),
('K30', 'DISPEPSIA'),
('K35', 'APENDICITIS AGUDA'),
('K350', 'APENDICITIS AGUDA CON PERITONITIS GENERALIZADA'),
('K703', 'CIRROSIS HEPATICA ALCOHOLICA'),
('K74', 'FIBROSIS Y CIRROSIS DEL HIGADO'),
('K80', 'COLELITIASIS'),
('L40', 'PSORIASIS'),
('L41', 'PARAPSORIASIS'),
('M090', 'ARTRITIS JUVENIL EN LA PSORIASIS (L40.5+)'),
('L50', 'URTICARIA'),
('L63', 'ALOPECIA AREATA'),
('Q840', 'ALOPECIA CONGENITA'),
('L93', 'LUPUS ERITEMATOSO'),
('M32', 'LUPUS ERITEMATOSO SISTEMICO'),
('N23', 'COLICO RENAL, NO ESPECIFICADO'),
('O15', 'ECLAMPSIA'),
('O149', 'PREECLAMPSIA, NO ESPECIFICADA'),
('T784', 'ALERGIA NO ESPECIFICADA'),
('Z88', 'HISTORIA PERSONAL DE ALERGIA A DROGAS, MEDICAMENTOS Y SUSTANCIAS BIOLOGICAS'),
('Z910', 'HISTORIA PERSONAL DE ALERGIA, NO DEBIDA A DROGAS NI A SUSTANCIAS BIOLOGICAS'),
('R51', 'CEFALEA'),
('G44', 'OTROS SINDROMES DE CEFALEA'),
('E756', 'TRASTORNO DEL ALMACENAMIENTO DE LIPIDOS, NO ESPECIFICADO'),
('E780', 'HIPERCOLESTEROLEMIA PURA'),
('N91', 'MENSTRUACION AUSENTE, ESCASA O RARA'),
('N926', 'MENSTRUACION IRREGULAR, NO ESPECIFICADA'),
('N953', 'ESTADOS ASOCIADOS CON MENOPAUSIA ARTIFICIAL'),
('N912', 'AMENORREA, SIN OTRA ESPECIFICACION'),
('R42', 'MAREO Y DESVANECIMIENTO'),
('T386', 'ANTIGONADOTROFINAS, ANTIESTROGENOS Y ANTIANDROGENOS, NO CLASIFICADOS EN OTR'),
('N910', 'AMENORREA PRIMARIA'),
('N912', 'AMENORREA, SIN OTRA ESPECIFICACION'),
('N911', 'AMENORREA SECUNDARIA'),
('R10', 'DOLOR ABDOMINAL Y PELVICO'),
('K590', 'CONSTIPACION'),
('L74', 'TRASTORNOS SUDORIPAROS ECRINOS'),
('L75', 'TRASTORNOS SUDORIPAROS APOCRINOS'),
('Y838', 'OTROS PROCEDIMIENTOS QUIRURGICOS'),
('N390', 'INFECCION DE VIAS URINARIAS, SITIO NO ESPECIFICADO'),
('O23', 'INFECCION DE LAS VIAS GENITOURINARIAS EN EL EMBARAZO'),
('N484', 'IMPOTENCIA DE ORIGEN ORGANICO'),
('K593', 'MEGACOLON, NO CLASIFICADO EN OTRA PARTE'),
('K931', 'MEGACOLON EN LA ENFERMEDAD DE CHAGAS (B57.3+)'),
('R501', 'FIEBRE PERSISTENTE'),
('M899', 'TRASTORNO DEL HUESO, NO ESPECIFICADO'),
('M545', 'LUMBAGO NO ESPECIFICADO'),
('M544', 'LUMBAGO CON CIATICA'),
('R100', 'ABDOMEN AGUDO'),
('I67', 'OTRAS ENFERMEDADES CEREBROVASCULARES'),
('I20', 'ANGINA DE PECHO'),
('I201', 'ANGINA DE PECHO CON ESPASMO DOCUMENTADO'),
('E010', 'BOCIO DIFUSO (ENDEMICO) RELACIONADO CON DEFICIENCIA DE YODO'),
('E011', 'BOCIO MULTINODULAR (ENDEMICO) RELACIONADO CON DEFICIENCIA DE YODO'),
('E030', 'HIPOTIROIDISMO CONGENITO CON BOCIO DIFUSO'),
('E04', 'OTRO BOCIO NO TOXICO'),
('P720', 'BOCIO NEONATAL, NO CLASIFICADO EN OTRA PARTE'),
('Z08', 'EXAMEN DE SEGUIMIENTO CONSECUTIVO AL TRATAMIENTO POR TUMOR MALIGNO'),
('L20', 'DERMATITIS ATOPICA'),
('L23', 'DERMATITIS ALERGICA DE CONTACTO'),
('L24', 'DERMATITIS DE CONTACTO POR IRRITANTES'),
('L26', 'DERMATITIS EXFOLIATIVA'),
('L30', 'OTRAS DERMATITIS'),
('R060', 'DISNEA'),
('R300', 'DISURIA'),
('R040', 'EPISTAXIS'),
('R160', 'HEPATOMEGALIA, NO CLASIFICADA EN OTRA PARTE'),
('R16', 'HEPATOMEGALIA Y ESPLENOMEGALIA, NO CLASIFICADAS EN OTRA PARTE'),
('K75', 'OTRAS ENFERMEDADES INFLAMATORIAS DEL HIGADO'),
('K76', 'OTRAS ENFERMEDADES DEL HIGADO'),
('N97', 'INFERTILIDAD FEMENINA'),
('A05', 'OTRAS INTOXICACIONES ALIMENTARIAS BACTERIANAS'),
('Y91', 'EVIDENCIA DE ALCOHOLISMO DETERMINADA POR EL NIVEL DE INTOXICACION'),
('N92', 'MENSTRUACION EXCESIVA, FRECUENTE E IRREGULAR'),
('M892', 'OTROS TRASTORNOS DEL DESARROLLO Y CRECIMIENTO OSEO'),
('M80', 'OSTEOPOROSIS CON FRACTURA PATOLOGICA'),
('M81', 'OSTEOPOROSIS SIN FRACTURA PATOLOGICA'),
('M82', 'OSTEOPOROSIS EN ENFERMEDADES CLASIFICADAS EN OTRA PARTE'),
('N110', 'PIELONEFRITIS CRONICA NO OBSTRUCTIVA ASOCIADA CON REFLUJO'),
('N111', 'PIELONEFRITIS CRONICA OBSTRUCTIVA'),
('N41', 'ENFERMEDADES INFLAMATORIAS DE LA PROSTATA'),
('N42', 'OTROS TRASTORNOS DE LA PROSTATA'),
('N40', 'HIPERPLASIA DE LA PROSTATA'),
('R59', 'ADENOMEGALIA'),
('E66', 'OBESIDAD'),
('R11', 'NAUSEA Y VOMITO'),
('O03', 'ABORTO ESPONTANEO'),
('L70', 'ACNE'),
('T784', 'ALERGIA NO ESPECIFICADA'),
('N970', 'INFERTILIDAD FEMENINA ASOCIADA CON FALTA DE OVULACION'),
('I200', 'ANGINA INESTABLE'),
('I49', 'OTRAS ARRITMIAS CARDIACAS'),
('M24', 'OTROS TRASTORNOS ARTICULARES ESPECIFICOS'),
('R634', 'PERDIDA ANORMAL DE PESO'),
('P050', 'BAJO PESO PARA LA EDAD GESTACIONAL'),
('P071', 'OTRO PESO BAJO AL NACER'),
('H10', 'CONJUNTIVITIS'),
('H104', 'CONJUNTIVITIS CRONICA'),
('B30', 'CONJUNTIVITIS VIRAL'),
('H102', 'OTRAS CONJUNTIVITIS AGUDAS'),
('Z95', 'PRESENCIA DE IMPLANTES E INJERTOS CARDIOVASCULARES'),
('E43', 'DESNUTRICION PROTEICOCALORICA SEVERA, NO ESPECIFICADA'),
('O25', 'DESNUTRICION EN EL EMBARAZO'),
('P05', 'RETARDO DEL CRECIMIENTO FETAL Y DESNUTRICION FETAL'),
('Y909', 'PRESENCIA DE ALCOHOL EN LA SANGRE, NIVEL NO ESPECIFICADO'),
('Y919', 'ALCOHOLISMO, NIVEL DE INTOXICACION NO ESPECIFICADO'),
('R60', 'EDEMA, NO CLASIFICADO EN OTRA PARTE'),
('R600', 'EDEMA LOCALIZADO'),
('R601', 'EDEMA GENERALIZADO'),
('A64', 'ENFERMEDAD DE TRANSMISION SEXUAL NO ESPECIFICADA'),
('EPOC - INSUFICIENCIA RESPIRATORIA', 'EPOC - INSUFICIENCIA RESPIRATORIA'),
('J98', 'OTROS TRASTORNOS RESPIRATORIOS'),
('M10', 'GOTA'),
('T810', 'HEMORRAGIA Y HEMATOMA QUE COMPLICAN UN PROCEDIMIENTO, NO CLASIFICADOS EN OT'),
('L680', 'HIRSUTISMO'),
('R17', 'ICTERICIA NO ESPECIFICADA'),
('P58', 'ICTERICIA NEONATAL DEBIDA A OTRAS HEMOLISIS EXCESIVAS'),
('P59', 'ICTERICIA NEONATAL POR OTRAS CAUSAS Y POR LAS NO ESPECIFICADAS'),
('C959', 'LEUCEMIA, NO ESPECIFICADA'),
('C91', 'LEUCEMIA LINFOIDE'),
('C92', 'LEUCEMIA MIELOIDE'),
('C93', 'LEUCEMIA MONOCITICA'),
('C963', 'LINFOMA HISTIOCITICO VERDADERO'),
('C859', 'LINFOMA NO HODGKIN, NO ESPECIFICADO'),
('C84', 'LINFOMA DE CELULAS T, PERIFERICO Y CUTANEO'),
('C83', 'LINFOMA NO HODGKIN DIFUSO'),
('C82', 'LINFOMA NO HODGKIN FOLICULAR [NODULAR]'),
('K80', 'COLELITIASIS'),
('E88', 'OTROS TRASTORNOS METABOLICOS'),
('M791', 'MIALGIA'),
('J189', 'NEUMONIA, NO ESPECIFICADA'),
('R631', 'POLIDIPSIA'),
('R072', 'DOLOR PRECORDIAL'),
('L29', 'PRURITO'),
('H82', 'SINDROMES VERTIGINOSOS EN ENFERMEDADES CLASIFICADAS EN OTRA PARTE'),
('A881', 'VERTIGO EPIDEMICO'),
('H814', 'VERTIGO DE ORIGEN CENTRAL'),
('A379', 'TOS FERINA, NO ESPECIFICADA'),
('E282', 'SINDROME DE OVARIO POLIQUISTICO'),
('E282', 'SINDROME DE OVARIO POLIQUISTICO'),
('Z34', 'SUPERVISION DE EMBARAZO NORMAL');
```

-  Tipos de paciente
```sql
INSERT INTO sis_tipo_paciente (tipo, descripcion) VALUES
('Paciente ambulatorio', 'Pacientes que reciben atención médica sin necesidad de hospitalización, ya sea en consultas externas, centros de salud, clínicas u hospitales de día. Esto incluye visitas para chequeos regulares, consultas por enfermedades crónicas o agudas, entre otros.'),
('Paciente hospitalizado', 'Pacientes que requieren internamiento en un hospital debido a la gravedad de su condición médica, para recibir tratamiento intensivo, cirugía, observación prolongada o cuidados especializados.'),
('Paciente crónico', 'Pacientes que padecen enfermedades crónicas, como diabetes, hipertensión, enfermedades cardiovasculares, entre otras, que requieren un manejo a largo plazo y seguimiento continuo para controlar la enfermedad y prevenir complicaciones.'),
('Paciente agudo', 'Pacientes que presentan enfermedades o condiciones médicas agudas que requieren atención inmediata y tratamiento urgente, como traumatismos, crisis asmáticas, infartos, accidentes cerebrovasculares, entre otros.'),
('Paciente pediátrico', 'Niños y adolescentes que reciben atención médica, ya sea en consulta ambulatoria o hospitalaria, con enfoque en las necesidades específicas de esta población.'),
('Paciente geriátrico', 'Adultos mayores que requieren atención médica especializada debido a las condiciones de salud asociadas con el envejecimiento, como enfermedades crónicas, fragilidad, deterioro cognitivo, entre otros.');
```

-  Formatos
```sql
INSERT INTO sis_formatos (codigo, descripcion) VALUES
('F001', 'Historia Clínica'),
('F002', 'Informe Médico'),
('F003', 'Receta Médica'),
('F004', 'Orden de Laboratorio'),
('F005', 'Orden de Radiografía'),
('F006', 'Orden de Ecografía'),
('F007', 'Orden de Tomografía'),
('F008', 'Orden de Resonancia Magnética'),
('F009', 'Orden de Endoscopía'),
('F010', 'Informe de Cirugía'),
('F011', 'Informe de Consulta Externa'),
('F012', 'Informe de Urgencias'),
('F013', 'Informe de Hospitalización'),
('F014', 'Informe de Alta Médica'),
('F015', 'Informe de Análisis de Laboratorio'),
('F016', 'Informe de Patología'),
('F017', 'Informe de Anatomía Patológica'),
('F018', 'Informe de Radiología'),
('F019', 'Informe de Cardiología'),
('F020', 'Informe de Neurología'),
('F021', 'Informe de Psicología'),
('F022', 'Informe de Nutrición'),
('F023', 'Informe de Fisioterapia'),
('F024', 'Informe de Terapia Ocupacional'),
('F025', 'Informe de Trabajo Social');
```
-  Usuarios
```sql
INSERT INTO sis_usuarios (usuario, pass, nombre_completo, ultimo_acceso, estado) VALUES
('jperez', CONVERT( VARCHAR(32), HASHBYTES('MD5', 'jperez'), 2 ), 'Juan Pérez', GETDATE(), 1),
('mmartinez', CONVERT( VARCHAR(32), HASHBYTES('MD5', 'mmartinez'), 2 ), 'María Martínez', GETDATE(), 1),
('aestrada', CONVERT( VARCHAR(32), HASHBYTES('MD5', 'aestrada'), 2 ), 'Andrés Estrada', GETDATE(), 1),
('pluna', CONVERT( VARCHAR(32), HASHBYTES('MD5', 'pluna'), 2 ), 'Pedro Luna', GETDATE(), 1),
('lsantos', CONVERT( VARCHAR(32), HASHBYTES('MD5', 'lsantos'), 2 ), 'Laura Santos', GETDATE(), 1),
('fgonzalez', CONVERT( VARCHAR(32), HASHBYTES('MD5', 'fgonzalez'), 2 ), 'Fernando González', GETDATE(), 1),
('dlopez', CONVERT( VARCHAR(32), HASHBYTES('MD5', 'dlopez'), 2 ), 'David López', GETDATE(), 1),
('mgomez', CONVERT( VARCHAR(32), HASHBYTES('MD5', 'mgomez'), 2 ), 'Marina Gómez', GETDATE(), 1),
('jrodriguez', CONVERT( VARCHAR(32), HASHBYTES('MD5', 'jrodriguez'), 2 ), 'Javier Rodríguez', GETDATE(), 1),
('pperez', CONVERT( VARCHAR(32), HASHBYTES('MD5', 'pperez'), 2 ), 'Patricia Pérez', GETDATE(), 1),
('rcastro', CONVERT( VARCHAR(32), HASHBYTES('MD5', 'rcastro'), 2 ), 'Roberto Castro', GETDATE(), 1),
('cmartinez', CONVERT( VARCHAR(32), HASHBYTES('MD5', 'cmartinez'), 2 ), 'Carolina Martínez', GETDATE(), 1),
('rlara', CONVERT( VARCHAR(32), HASHBYTES('MD5', 'rlara'), 2 ), 'Raúl Lara', GETDATE(), 1),
('vramirez', CONVERT( VARCHAR(32), HASHBYTES('MD5', 'vramirez'), 2 ), 'Verónica Ramírez', GETDATE(), 1),
('rgarcia', CONVERT( VARCHAR(32), HASHBYTES('MD5', 'rgarcia'), 2 ), 'Rosa García', GETDATE(), 1),
('jcastillo', CONVERT( VARCHAR(32), HASHBYTES('MD5', 'jcastillo'), 2 ), 'Juan Castillo', GETDATE(), 1),
('esilva', CONVERT( VARCHAR(32), HASHBYTES('MD5', 'esilva'), 2 ), 'Elena Silva', GETDATE(), 1),
('darias', CONVERT( VARCHAR(32), HASHBYTES('MD5', 'darias'), 2 ), 'Daniel Arias', GETDATE(), 1),
('esantana', CONVERT( VARCHAR(32), HASHBYTES('MD5', 'esantana'), 2 ), 'Eva Santana', GETDATE(), 1),
('jgutierrez', CONVERT( VARCHAR(32), HASHBYTES('MD5', 'jgutierrez'), 2 ), 'José Gutiérrez', GETDATE(), 1),
('mmendez', CONVERT( VARCHAR(32), HASHBYTES('MD5', 'mmendez'), 2 ), 'Mónica Méndez', GETDATE(), 1),
('jvasquez', CONVERT( VARCHAR(32), HASHBYTES('MD5', 'jvasquez'), 2 ), 'Julia Vásquez', GETDATE(), 1),
('asanchez', CONVERT( VARCHAR(32), HASHBYTES('MD5', 'asanchez'), 2 ), 'Antonio Sánchez', GETDATE(), 1),
('nfernandez', CONVERT( VARCHAR(32), HASHBYTES('MD5', 'nfernandez'), 2 ), 'Natalia Fernández', GETDATE(), 1),
('msantos', CONVERT( VARCHAR(32), HASHBYTES('MD5', 'msantos'), 2 ), 'Manuel Santos', GETDATE(), 1),
('cnavarro', CONVERT( VARCHAR(32), HASHBYTES('MD5', 'cnavarro'), 2 ), 'Carmen Navarro', GETDATE(), 1),
('lsanchez', CONVERT( VARCHAR(32), HASHBYTES('MD5', 'lsanchez'), 2 ), 'Luis Sánchez', GETDATE(), 1),
('jcabrera', CONVERT( VARCHAR(32), HASHBYTES('MD5', 'jcabrera'), 2 ), 'Juana Cabrera', GETDATE(), 1),
('fdiaz', CONVERT( VARCHAR(32), HASHBYTES('MD5', 'fdiaz'), 2 ), 'Fabián Díaz', GETDATE(), 1),
('asalazar', CONVERT( VARCHAR(32), HASHBYTES('MD5', 'asalazar'), 2 ), 'Ana Salazar', GETDATE(), 1),
('mreyes', CONVERT( VARCHAR(32), HASHBYTES('MD5', 'mreyes'), 2 ), 'Marcela Reyes', GETDATE(), 1),
('emartinez', CONVERT( VARCHAR(32), HASHBYTES('MD5', 'emartinez'), 2 ), 'Eduardo Martínez', GETDATE(), 1),
('cromo', CONVERT( VARCHAR(32), HASHBYTES('MD5', 'cromo'), 2 ), 'Cristina Romo', GETDATE(), 1),
('apalacios', CONVERT( VARCHAR(32), HASHBYTES('MD5', 'apalacios'), 2 ), 'Alejandro Palacios', GETDATE(), 1),
('lfernandez', CONVERT( VARCHAR(32), HASHBYTES('MD5', 'lfernandez'), 2 ), 'Lorena Fernández', GETDATE(), 1),
('gchavez', CONVERT( VARCHAR(32), HASHBYTES('MD5', 'gchavez'), 2 ), 'Gabriel Chávez', GETDATE(), 1),
('jflores', CONVERT( VARCHAR(32), HASHBYTES('MD5', 'jflores'), 2 ), 'Julieta Flores', GETDATE(), 1),
('cgomez', CONVERT( VARCHAR(32), HASHBYTES('MD5', 'cgomez'), 2 ), 'Carlos Gómez', GETDATE(), 1),
('esteban', CONVERT( VARCHAR(32), HASHBYTES('MD5', 'esteban'), 2 ), 'Estela Benítez', GETDATE(), 1),
('mvalencia', CONVERT( VARCHAR(32), HASHBYTES('MD5', 'mvalencia'), 2 ), 'Miguel Valencia', GETDATE(), 1),
('rsalinas', CONVERT( VARCHAR(32), HASHBYTES('MD5', 'rsalinas'), 2 ), 'Rocio Salinas', GETDATE(), 1),
('mperez', CONVERT( VARCHAR(32), HASHBYTES('MD5', 'mperez'), 2 ), 'Mario Pérez', GETDATE(), 1),
('vsuarez', CONVERT( VARCHAR(32), HASHBYTES('MD5', 'vsuarez'), 2 ), 'Victoria Suárez', GETDATE(), 1),
('jrivas', CONVERT( VARCHAR(32), HASHBYTES('MD5', 'jrivas'), 2 ), 'Juan Rivas', GETDATE(), 1),
('msilva', CONVERT( VARCHAR(32), HASHBYTES('MD5', 'msilva'), 2 ), 'Mercedes Silva', GETDATE(), 1),
('rluna', CONVERT( VARCHAR(32), HASHBYTES('MD5', 'rluna'), 2 ), 'Ramón Luna', GETDATE(), 1),
('evelasquez', CONVERT( VARCHAR(32), HASHBYTES('MD5', 'evelasquez'), 2 ), 'Eduarda Velásquez', GETDATE(), 1),
('osantana', CONVERT( VARCHAR(32), HASHBYTES('MD5', 'osantana'), 2 ), 'Óscar Santana', GETDATE(), 1),
('mmolina', CONVERT( VARCHAR(32), HASHBYTES('MD5', 'mmolina'), 2 ), 'Martha Molina', GETDATE(), 1),
('jmejia', CONVERT( VARCHAR(32), HASHBYTES('MD5', 'jmejia'), 2 ), 'José Mejía', GETDATE(), 1);
```

-  Médicos
```sql
INSERT INTO sis_medico ( cedula, nombre, especialidad_id, registro, tipo_id, tiempo, cod_usuario, es_medico, es_anes, es_ayu, pago_prod, valoresperado, es_pediatra, servicio_id, abre_historia, cierra_historia, es_auditor, es_especialista, estado, tercero, ApartaCita, direccion, telefono, citaExterna, leyendaConfirmarMedico, RequiereAuditoria, NivelMctos, CodHistoriaPredeterminada, EsMedicoFamiliar, EsOdontologo, EsPyp ) VALUES
(123456789, 'Juan Pérez', 1, 12345, 1, 40, 1, 1, 0, 0, 0, 0, 0, 1, 1, 1, 0, 1, 1, 0, 0, 'Calle 123 #456', 1234567890, 0, NULL, 0, 1, NULL, 0, 0, 1),
(234567890, 'María Martínez', 2, 23456, 2, 45, 2, 1, 0, 0, 0, 0, 0, 1, 1, 1, 0, 1, 1, 0, 0, 'Carrera 45 #678', 2345678901, 0, NULL, 0, 1, NULL, 0, 0, 1),
(345678901, 'Andrés Estrada', 3, 34567, 3, 50, 3, 1, 0, 0, 0, 0, 0, 1, 1, 1, 0, 1, 1, 0, 0, 'Avenida 678 #901', 3456789012, 0, NULL, 0, 1, NULL, 0, 0, 1),
(456789012, 'Pedro Luna', 4, 45678, 4, 55, 4, 1, 0, 0, 0, 0, 0, 1, 1, 1, 0, 1, 1, 0, 0, 'Transversal 89 #012', 4567890123, 0, NULL, 0, 1, NULL, 0, 0, 1),
(567890123, 'Laura Santos', 5, 56789, 5, 60, 5, 1, 0, 0, 0, 0, 0, 1, 1, 1, 0, 1, 1, 0, 0, 'Carrera 01 #234', 5678901234, 0, NULL, 0, 1, NULL, 0, 0, 1),
(678901234, 'Fernando González', 6, 67890, 6, 65, 6, 1, 0, 0, 0, 0, 0, 1, 1, 1, 0, 1, 1, 0, 0, 'Calle 12 #345', 6789012345, 0, NULL, 0, 1, NULL, 0, 0, 1),
(789012345, 'David López', 7, 78901, 7, 70, 7, 1, 0, 0, 0, 0, 0, 1, 1, 1, 0, 1, 1, 0, 0, 'Avenida 23 #456', 7890123456, 0, NULL, 0, 1, NULL, 0, 0, 1),
(890123456, 'Marina Gómez', 8, 89012, 8, 75, 8, 1, 0, 0, 0, 0, 0, 1, 1, 1, 0, 1, 1, 0, 0, 'Transversal 34 #567', 8901234567, 0, NULL, 0, 1, NULL, 0, 0, 1),
(901234567, 'Javier Rodríguez', 9, 90123, 9, 80, 9, 1, 0, 0, 0, 0, 0, 1, 1, 1, 0, 1, 1, 0, 0, 'Carrera 45 #678', 9012345678, 0, NULL, 0, 1, NULL, 0, 0, 1),
(123450987, 'Patricia Pérez', 10, 12345, 10, 85, 10, 1, 0, 0, 0, 0, 0, 1, 1, 1, 0, 1, 1, 0, 0, 'Calle 67 #890', 1234509876, 0, NULL, 0, 1, NULL, 0, 0, 1),
(234509876, 'Carlos Gómez', 1, 23456, 1, 90, 38, 1, 0, 0, 0, 0, 0, 1, 1, 1, 0, 1, 1, 0, 0, 'Avenida 89 #012', 2345098765, 0, NULL, 0, 1, NULL, 0, 0, 1),
(345098765, 'Carolina Martínez', 2, 34567, 2, 95, 12, 1, 0, 0, 0, 0, 0, 1, 1, 1, 0, 1, 1, 0, 0, 'Transversal 90 #123', 3450987654, 0, NULL, 0, 1, NULL, 0, 0, 1),
(450987654, 'Raúl Lara', 3, 45678, 3, 100, 13, 1, 0, 0, 0, 0, 0, 1, 1, 1, 0, 1, 1, 0, 0, 'Carrera 12 #345', 4509876543, 0, NULL, 0, 1, NULL, 0, 0, 1),
(509876543, 'Verónica Ramírez', 4, 56789, 4, 105, 14, 1, 0, 0, 0, 0, 0, 1, 1, 1, 0, 1, 1, 0, 0, 'Calle 23 #456', 5098765432, 0, NULL, 0, 1, NULL, 0, 0, 1),
(098765432, 'Rosa García', 5, 67890, 5, 110, 15, 1, 0, 0, 0, 0, 0, 1, 1, 1, 0, 1, 1, 0, 0, 'Avenida 34 #567', 0987654321, 0, NULL, 0, 1, NULL, 0, 0, 1),
(987224321, 'Juan Castillo', 6, 78901, 6, 115, 16, 1, 0, 0, 0, 0, 0, 1, 1, 1, 0, 1, 1, 0, 0, 'Transversal 45 #678', 9876543210, 0, NULL, 0, 1, NULL, 0, 0, 1),
(876543210, 'Elena Silva', 7, 89012, 7, 120, 17, 1, 0, 0, 0, 0, 0, 1, 1, 1, 0, 1, 1, 0, 0, 'Carrera 56 #789', 8765432109, 0, NULL, 0, 1, NULL, 0, 0, 1),
(765432109, 'Daniel Arias', 8, 90123, 8, 125, 18, 1, 0, 0, 0, 0, 0, 1, 1, 1, 0, 1, 1, 0, 0, 'Calle 67 #890', 7654321098, 0, NULL, 0, 1, NULL, 0, 0, 1),
(654321098, 'Eva Santana', 9, 12345, 9, 130, 19, 1, 0, 0, 0, 0, 0, 1, 1, 1, 0, 1, 1, 0, 0, 'Avenida 78 #901', 6543210987, 0, NULL, 0, 1, NULL, 0, 0, 1),
(543210987, 'José Gutiérrez', 10, 23456, 10, 135, 20, 1, 0, 0, 0, 0, 0, 1, 1, 1, 0, 1, 1, 0, 0, 'Transversal 89 #012', 5432109876, 0, NULL, 0, 1, NULL, 0, 0, 1),
(432109876, 'Mónica Méndez', 1, 34567, 1, 140, 21, 1, 0, 0, 0, 0, 0, 1, 1, 1, 0, 1, 1, 0, 0, 'Carrera 90 #123', 4321098765, 0, NULL, 0, 1, NULL, 0, 0, 1),
(321098765, 'Julia Vásquez', 2, 45678, 2, 145, 22, 1, 0, 0, 0, 0, 0, 1, 1, 1, 0, 1, 1, 0, 0, 'Calle 12 #345', 3210987654, 0, NULL, 0, 1, NULL, 0, 0, 1),
(210987654, 'Antonio Sánchez', 3, 56789, 3, 150, 23, 1, 0, 0, 0, 0, 0, 1, 1, 1, 0, 1, 1, 0, 0, 'Avenida 23 #456', 2109876543, 0, NULL, 0, 1, NULL, 0, 0, 1),
(109876543, 'Natalia Fernández', 4, 67890, 4, 155, 24, 1, 0, 0, 0, 0, 0, 1, 1, 1, 0, 1, 1, 0, 0, 'Transversal 34 #567', 1098765432, 0, NULL, 0, 1, NULL, 0, 0, 1),
(012345678, 'Manuel Santos', 5, 78901, 5, 160, 25, 1, 0, 0, 0, 0, 0, 1, 1, 1, 0, 1, 1, 0, 0, 'Carrera 45 #678', 0123456789, 0, NULL, 0, 1, NULL, 0, 0, 1),
(0987654321, 'Carmen Navarro', 6, 89012, 6, 165, 26, 1, 0, 0, 0, 0, 0, 1, 1, 1, 0, 1, 1, 0, 0, 'Calle 67 #890', 0987654321, 0, NULL, 0, 1, NULL, 0, 0, 1),
(9221543210, 'Luis Sánchez', 7, 90123, 7, 170, 27, 1, 0, 0, 0, 0, 0, 1, 1, 1, 0, 1, 1, 0, 0, 'Avenida 78 #901', 3276543210, 0, NULL, 0, 1, NULL, 0, 0, 1),
(8765432109, 'Juana Cabrera', 8, 12345, 8, 175, 28, 1, 0, 0, 0, 0, 0, 1, 1, 1, 0, 1, 1, 0, 0, 'Transversal 89 #012', 8765432109, 0, NULL, 0, 1, NULL, 0, 0, 1),
(7654321098, 'Fabián Díaz', 9, 23456, 9, 180, 29, 1, 0, 0, 0, 0, 0, 1, 1, 1, 0, 1, 1, 0, 0, 'Carrera 90 #123', 7654321098, 0, NULL, 0, 1, NULL, 0, 0, 1),
(6543210987, 'Ana Salazar', 10, 34567, 10, 185, 30, 1, 0, 0, 0, 0, 0, 1, 1, 1, 0, 1, 1, 0, 0, 'Calle 12 #345', 6543210987, 0, NULL, 0, 1, NULL, 0, 0, 1),
(5432109876, 'Marcela Reyes', 1, 45678, 1, 190, 31, 1, 0, 0, 0, 0, 0, 1, 1, 1, 0, 1, 1, 0, 0, 'Avenida 23 #456', 5432109876, 0, NULL, 0, 1, NULL, 0, 0, 1),
(4321098765, 'Eduardo Martínez', 2, 56789, 2, 195, 32, 1, 0, 0, 0, 0, 0, 1, 1, 1, 0, 1, 1, 0, 0, 'Transversal 34 #567', 4321098765, 0, NULL, 0, 1, NULL, 0, 0, 1),
(3210987654, 'Cristina Romo', 3, 67890, 3, 200, 33, 1, 0, 0, 0, 0, 0, 1, 1, 1, 0, 1, 1, 0, 0, 'Carrera 45 #678', 3210987654, 0, NULL, 0, 1, NULL, 0, 0, 1),
(2109876543, 'Alejandro Palacios', 4, 78901, 4, 205, 34, 1, 0, 0, 0, 0, 0, 1, 1, 1, 0, 1, 1, 0, 0, 'Calle 67 #890', 2109876543, 0, NULL, 0, 1, NULL, 0, 0, 1),
(1098765432, 'Lorena Fernández', 5, 89012, 5, 210, 35, 1, 0, 0, 0, 0, 0, 1, 1, 1, 0, 1, 1, 0, 0, 'Avenida 78 #901', 1098765432, 0, NULL, 0, 1, NULL, 0, 0, 1),
(1234567890, 'Gabriel Chávez', 6, 90123, 6, 215, 36, 1, 0, 0, 0, 0, 0, 1, 1, 1, 0, 1, 1, 0, 0, 'Transversal 89 #012', 1234567890, 0, NULL, 0, 1, NULL, 0, 0, 1),
(2345678901, 'Julieta Flores', 7, 12345, 7, 220, 37, 1, 0, 0, 0, 0, 0, 1, 1, 1, 0, 1, 1, 0, 0, 'Carrera 90 #123', 2345678901, 0, NULL, 0, 1, NULL, 0, 0, 1),
(3456789012, 'Carlos Gómez', 8, 23456, 8, 225, 38, 1, 0, 0, 0, 0, 0, 1, 1, 1, 0, 1, 1, 0, 0, 'Calle 12 #345', 3456789012, 0, NULL, 0, 1, NULL, 0, 0, 1),
(4567890123, 'Estela Benítez', 9, 34567, 9, 230, 39, 1, 0, 0, 0, 0, 0, 1, 1, 1, 0, 1, 1, 0, 0, 'Avenida 23 #456', 4567890123, 0, NULL, 0, 1, NULL, 0, 0, 1),
(5678901234, 'Miguel Valencia', 10, 45678, 10, 235, 40, 1, 0, 0, 0, 0, 0, 1, 1, 1, 0, 1, 1, 0, 0, 'Transversal 34 #567', 5678901234, 0, NULL, 0, 1, NULL, 0, 0, 1);
```
