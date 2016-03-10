# pva_ign
# pva_ign 
Consolidation par region des geojson générés par cquest dans une table postgis (lambert 93)

http://si.cenlr.org/trouver_les_photos_anciennes_de_l_ign

-> https://github.com/cquest/photos-aeriennes-ign/tree/master/data/pva
-> http://georezo.net/forum/viewtopic.php?pid=279360#p279360

Les dumps contiennent une table PostGIS ayant la structure suivante : 
```sql
CREATE TABLE pva_nom_region
(
  gid integer,
  idcliche text,
  mission text,
  numcli text,
  idta text,
  date text,
  res text,
  support text,
  type text,
  surface double precision,
  lon double precision,
  lat double precision,
  orientation text,
  url text,
  largeur integer,
  hauteur integer,
  taille integer,
  geometrie geometry(Polygon,2154)
  );
  ```
  
  Libre à vous de créer la clé primaire et les index.
  ```sql
  ALTER TABLE pva_nom_region ADD CONSTRAINT pva_pk PRIMARY KEY(gid);
  CREATE INDEX pva_geometrie_idx ON pva USING gist (geometrie);
```

La fonction à utiliser dans l'action "ouvrir fichier" pour télécharger ces images depuis QGis (Merci David ;-)):
```sql
'http://wxs.ign.fr/cle_d_acces/jp2/DEMAT.PVA/'||"mission"||'/'|| "url"
```

Les dumps sont ici : www.cenlr.org/divers/pva
