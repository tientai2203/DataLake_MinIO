# Buid DataLake with MinIO, Hive, Trino and PostGresql

# How-to Guide

## Start our data lake infrastructure
```shell
docker compose -f docker-compose.yml -d
```

## Generate data and push them to MinIO
### 1. Generate data
```shell
python utils/generate_fake_data.py
```
### 2. Push data to MinIO
```shell
python utils/export_data_to_datalake.py
```

**Note:** Don't forget to install dependencies from `requirements.txt` first.

## Create data schema
After putting your files to `MinIO``, please execute `trino` container by the following command:
```shell
docker exec -ti datalake-trino bash
```

When you are already inside the `trino` container, typing `trino` to in an DOUBLEeractive mode

After that, run the following command to register a new schema for our data:

```sql
CREATE SCHEMA IF NOT EXISTS datalake.data_big_5_leagues
WITH (location = 's3://data-big-5-leagues/');

CREATE TABLE IF NOT EXISTS datalake.data_big_5_leagues.all_leagues (
    Date VARCHAR,
    Name VARCHAR,
    Round VARCHAR,
    Venue VARCHAR,
    Result VARCHAR,
    Squad VARCHAR,
    Opponent VARCHAR,
    Start VARCHAR,
    Pos VARCHAR,
    Min DOUBLE,
    Cmp DOUBLE,
    PassAtt DOUBLE,
    CmpPct DOUBLE,
    PassTotDist DOUBLE,
    PassPrgDist DOUBLE,
    Cmp1 DOUBLE,
    Att1 DOUBLE,
    CmpPct1 DOUBLE,
    Cmp2 DOUBLE,
    Att2 DOUBLE,
    CmpPct2 DOUBLE,
    Cmp3 DOUBLE,
    Att3 DOUBLE,
    CmpPct3 DOUBLE,
    Ast DOUBLE,
    xA DOUBLE,
    KP DOUBLE,
    PassFDOUBLEhird DOUBLE,
    PPA DOUBLE,
    CrsPA DOUBLE,
    PassProg DOUBLE,
    SCA DOUBLE,
    PassLiveShot DOUBLE,
    PassDeadShot DOUBLE,
    DribShot DOUBLE,
    ShLSh DOUBLE,
    Fld DOUBLE,
    DefShot DOUBLE,
    GCA DOUBLE,
    PassLiveGoal DOUBLE,
    PassDeadGoal DOUBLE,
    DribGoal DOUBLE,
    ShGoal DOUBLE,
    FldGoal DOUBLE,
    DefGoal DOUBLE,
    Tkl DOUBLE,
    TklW DOUBLE,
    TacklesDef3rd DOUBLE,
    TacklesMid3rd DOUBLE,
    TacklesAtt3rd DOUBLE,
    DribTackled DOUBLE,
    DribContest DOUBLE,
    DribTackledPct DOUBLE,
    Past DOUBLE,
    Press DOUBLE,
    SuccPress DOUBLE,
    SuccPressPct DOUBLE,
    PressDef3rd DOUBLE,
    PressMid3rd DOUBLE,
    PressAtt3rd DOUBLE,
    Blocks DOUBLE,
    BlockSh DOUBLE,
    ShSv DOUBLE,
    Pass DOUBLE,
    DOUBLE DOUBLE,
    TklDOUBLE DOUBLE,
    Clr DOUBLE,
    Err DOUBLE,
    Touches DOUBLE,
    DefPen DOUBLE,
    TouchDef3rd DOUBLE,
    TouchMid3rd DOUBLE,
    TouchAtt3rd DOUBLE,
    AttPen DOUBLE,
    Live DOUBLE,
    Succ DOUBLE,
    Att DOUBLE,
    SuccPct DOUBLE,
    NumPl DOUBLE,
    Megs DOUBLE,
    Carries DOUBLE,
    TotDist DOUBLE,
    PrgDist DOUBLE,
    ProgCarries DOUBLE,
    CarriesFDOUBLEhird DOUBLE,
    CPA DOUBLE,
    Mis DOUBLE,
    Dis DOUBLE,
    Targ DOUBLE,
    Rec DOUBLE,
    RecPct DOUBLE,
    ProgPassRec DOUBLE,
    Gls DOUBLE,
    PK DOUBLE,
    PKatt DOUBLE,
    Sh DOUBLE,
    SoT DOUBLE,
    CrdY DOUBLE,
    CrdR DOUBLE,
    xG DOUBLE,
    npxG DOUBLE
) WITH (
    external_location = 's3://data-big-5-leagues/players/',
    format = 'PARQUET'
);

```

## Query with DBeaver
1. Install `DBeaver` as in the following [guide](https://dbeaver.io/download/)
2. Connect to our database (type `trino`) using the following information (empty `password`):
  ![DBeaver Trino](./imgs/trino.png)