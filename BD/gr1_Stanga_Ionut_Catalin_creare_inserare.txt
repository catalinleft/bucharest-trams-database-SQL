create sequence seq_depou
start with 1
increment by 1
nocache;

CREATE TABLE Depou(
    id_depou INT NOT NULL,
    nume VARCHAR2(20),
    adresa VARCHAR(40),
    capacitate INT,
    sector INT,
    CONSTRAINT pk_depou PRIMARY KEY (id_depou)
);

CREATE TABLE SefDepou (
    id_sef_depou INT NOT NULL,
    id_depou INT,
    nume VARCHAR(30),
    telefon VARCHAR(11),
    CONSTRAINT pk_sefdepou PRIMARY KEY (id_sef_depou),
    CONSTRAINT fk_sefdepou FOREIGN KEY (id_depou) REFERENCES Depou(id_depou)
);

CREATE TABLE Tramvai (
    numar_vagon INT NOT NULL,
    id_depou INT,
    numar_scaune INT,
    model_vagon VARCHAR2(20),
    data_revizie DATE,
    CONSTRAINT pk_tramvai PRIMARY KEY (numar_vagon),
    CONSTRAINT fk_tramvai FOREIGN KEY (id_depou) REFERENCES Depou(id_depou)
);

CREATE TABLE Vatman (
    id_vatman INT NOT NULL,
    numar_vagon INT,
    nume VARCHAR2(30),
    experienta INT,
    salariu INT,
    CONSTRAINT pk_vatman PRIMARY KEY (id_vatman),
    CONSTRAINT fk_vatman FOREIGN KEY (numar_vagon) REFERENCES Tramvai(numar_vagon)
);

CREATE TABLE Linie (
    numar_linie INT NOT NULL,
    numar_tramvaie INT,
    statie_start VARCHAR2(20),
    statie_stop VARCHAR2(20),
    necesita_bidirectionale VARCHAR2(3),
    CONSTRAINT pk_linie PRIMARY KEY (numar_linie)
);

CREATE TABLE Statie (
    nume_statie VARCHAR2(20) NOT NULL,
    lungime_peron INT,
    sector INT,
    nr_calatori INT,
    nr_linii INT,
    legatura_metrou VARCHAR2(3),
    CONSTRAINT pk_statie PRIMARY KEY (nume_statie)
);

CREATE TABLE Alimenteaza (
    numar_vagon INT NOT NULL,
    numar_linie INT NOT NULL,
    CONSTRAINT pk_alimenteaza PRIMARY KEY (numar_vagon, numar_linie),
    CONSTRAINT fk1_alimenteaza FOREIGN KEY (numar_vagon) REFERENCES Tramvai (numar_vagon),
    CONSTRAINT fk2_alimenteaza FOREIGN KEY (numar_linie) REFERENCES Linie(numar_linie)
);

CREATE TABLE Deserveste (
    nume_statie VARCHAR2(20) NOT NULL,
    numar_linie INT NOT NULL,
    CONSTRAINT pk_deserveste PRIMARY KEY (nume_statie, numar_linie),
    CONSTRAINT fk1_deserveste FOREIGN KEY (nume_statie) REFERENCES Statie (nume_statie),
    CONSTRAINT fk2_deserveste FOREIGN KEY (numar_linie) REFERENCES Linie (numar_linie)
);

INSERT INTO Depou VALUES (seq_depou.nextval-1,'Militari' , 'Str. Preciziei 19-21' , 84 , 6);
INSERT INTO Depou VALUES (seq_depou.nextval-1,'Dudesti' , 'Calea Dudesti 184' , 65 , 3);
INSERT INTO Depou VALUES (seq_depou.nextval-1,'Colentina' , 'Sos. Colentina 278' , 35 , 2);
INSERT INTO Depou VALUES (seq_depou.nextval-1,'Alexandria' , 'Sos. Alexandria 5' , 70 , 5);
INSERT INTO Depou VALUES (seq_depou.nextval-1,'Victoria' , 'Str. Mexic 19' , 84 , 1);
INSERT INTO Depou VALUES (seq_depou.nextval-1,'Bucurestii Noi' , 'Bd. Bucurestii Noi 42' , 25 , 1);

INSERT INTO SefDepou VALUES (1, 3 , 'Caramfil Stefan' , '0700000001');
INSERT INTO SefDepou VALUES (2, 4 , 'Nitu Ioan' , '0700000002');
INSERT INTO SefDepou VALUES (3, 5 , 'Stoica Laurentiu' , '0700000003');
INSERT INTO SefDepou VALUES (4, 1 , 'Szabo George' , '0700000004');
INSERT INTO SefDepou VALUES (5, 6 , 'Pancu Dumitru' , '0700000005');
INSERT INTO SefDepou VALUES (6, 2 , 'Dobre Mihai' , '0700000006');

INSERT INTO Tramvai VALUES (39, 5 , 28 , 'V3A-93-2S', TO_DATE('2022-11-26','yyyy-mm-dd'));
INSERT INTO Tramvai VALUES (104, 5 , 25 , 'V3A-93-2S', TO_DATE('2022-08-13','yyyy-mm-dd'));
INSERT INTO Tramvai VALUES (77, 1 , 16 , 'TATRA T4R', TO_DATE('2020-08-03','yyyy-mm-dd'));
INSERT INTO Tramvai VALUES (78, 2 , 28 , 'V3A-93', TO_DATE('2022-11-26','yyyy-mm-dd'));
INSERT INTO Tramvai VALUES (1001, 1 , 44 , 'Astra Imperio', TO_DATE('2023-04-15','yyyy-mm-dd'));
INSERT INTO Tramvai VALUES (1002, 1 , 44 , 'Astra Imperio', TO_DATE('2023-04-17','yyyy-mm-dd'));
INSERT INTO Tramvai VALUES (13, 2 , 39 , 'Bucur LF', TO_DATE('2022-12-04','yyyy-mm-dd'));
INSERT INTO Tramvai VALUES (202, 4 , 26 , 'V3A-93-PPC', TO_DATE('2023-02-16','yyyy-mm-dd'));
INSERT INTO Tramvai VALUES (216, 6 , 26 , 'V3A-93-PPC', TO_DATE('2023-03-06','yyyy-mm-dd'));
INSERT INTO Tramvai VALUES (345, 3 , 28 , 'V3A-93', TO_DATE('2022-11-26','yyyy-mm-dd'));

INSERT INTO Vatman VALUES (1, 345 , 'Vasile Andrei' , 12 , 9800);
INSERT INTO Vatman VALUES (2, 77 , 'Popescu Stelian' , 7 , 8400);
INSERT INTO Vatman VALUES (3, 1001 , 'Stancu Alexandra' , 10 , 9000);
INSERT INTO Vatman VALUES (4, 1002 , 'Ignat Lenuta' , 1 , 5500);
INSERT INTO Vatman VALUES (5, 216 , 'Delea Daniel' , 5 , 7600);
INSERT INTO Vatman VALUES (6, 13 , 'Ionescu Paul' , 11 , 9300);
INSERT INTO Vatman VALUES (7, 39 , 'Sandu Camelia' , 2 , 5600);
INSERT INTO Vatman VALUES (8, 104 , 'Diaconescu Denis' , 5 , 7600);
INSERT INTO Vatman VALUES (9, 202 , 'Georgescu Victor' , 8 , 8800);
INSERT INTO Vatman VALUES (10, 78 , 'Vanea Gabriel' , 4 , 6600);
INSERT INTO Vatman VALUES (12, NULL , 'Eftimie Ioan' , 0 , 5000);
INSERT INTO Vatman VALUES (13, NULL , 'Militaru Ionela' , 3 , 6300);

INSERT INTO Linie VALUES (1, 2, 'Romprim', 'Banu Manta', 'NU');
INSERT INTO Linie VALUES (41, 2, 'Ghencea', 'Piata Presei', 'NU');
INSERT INTO Linie VALUES (44, 2, 'Cartier 16 februarie', 'Vasile Parvan', 'NU');
INSERT INTO Linie VALUES (5, 2, 'Piata Sf. Gheorghe', 'Piata Baneasa', 'DA');
INSERT INTO Linie VALUES (21, 1 , 'Romprim', 'Banu Manta', 'NU');
INSERT INTO Linie VALUES (32, 1, 'Piata Unirii', 'Dep. Alexandria', 'NU');

INSERT INTO Statie VALUES ( 'Bd. Lacul Tei', 30, 2, 1500, 1, 'NU');
INSERT INTO Statie VALUES ( 'Sos. Progresu', 70, 5, 13000, 2, 'NU');
INSERT INTO Statie VALUES ( 'Piata Crangasi', 30, 6, 35000, 1, 'DA');
INSERT INTO Statie VALUES ( 'Piata Obor', 30, 2, 22000, 2, 'DA');
INSERT INTO Statie VALUES ( 'Gradina Cismigiu', 0, 1, 250, 1, 'NU');
INSERT INTO Statie VALUES ( 'Gara Basarab', 45, 6, 10000, 2, 'DA');
INSERT INTO Statie VALUES ( 'Piata Gemeni', 0, 3, 1000, 1, 'NU');
INSERT INTO Statie VALUES ( 'Godeni', 0, 6, 750, 1, 'NU');
INSERT INTO Statie VALUES ( 'Piata Muncii', 35, 4, 18000, 1, 'DA');
INSERT INTO Statie VALUES ( 'Piata Unirii', 30, 5, 29000, 1, 'DA');

INSERT INTO Alimenteaza VALUES (13,1);
INSERT INTO Alimenteaza VALUES (78,1);
INSERT INTO Alimenteaza VALUES (1001,41);
INSERT INTO Alimenteaza VALUES (1002,41);
INSERT INTO Alimenteaza VALUES (77,44);
INSERT INTO Alimenteaza VALUES (216,44);
INSERT INTO Alimenteaza VALUES (39,5);
INSERT INTO Alimenteaza VALUES (104,5);
INSERT INTO Alimenteaza VALUES (345,21);
INSERT INTO Alimenteaza VALUES (202,32);

INSERT INTO Deserveste VALUES ('Bd. Lacul Tei',5);
INSERT INTO Deserveste VALUES ('Sos. Progresu',1);
INSERT INTO Deserveste VALUES ('Sos. Progresu',32);
INSERT INTO Deserveste VALUES ('Piata Crangasi',41);
INSERT INTO Deserveste VALUES ('Piata Obor',21);
INSERT INTO Deserveste VALUES ('Piata Obor',1);
INSERT INTO Deserveste VALUES ('Gradina Cismigiu',44);
INSERT INTO Deserveste VALUES ('Gara Basarab',1);
INSERT INTO Deserveste VALUES ('Gara Basarab',44);
INSERT INTO Deserveste VALUES ('Piata Gemeni',5);
INSERT INTO Deserveste VALUES ('Godeni',44);
INSERT INTO Deserveste VALUES ('Piata Muncii',1);
INSERT INTO Deserveste VALUES ('Piata Unirii',32);

drop sequence seq_depou;
