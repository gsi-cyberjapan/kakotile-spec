# kakotile-spec
Specifications for kakotile - metadata tileset for backup tiles

Kakotile tileset is a metadata tileset for backup tiles generated using [qdltc](https://github.com/gsi-cyberjapan/qdltc/). This document explains the specifications for backup tiles first, and then the specifications for kakotile.

By the way, kako (過去) means the past in Japanese language.

# Backup tileset
Backup tileset contains old tiles. The backup tile of the original tile at
```
{t}/{z}/{x}/{y}.{ext}
```
is stored as
```
{t}/bak/{z}/{x}/{y}.{date}.{ext}
```
where {date} is the modification date (mtime) of the original tile.

# Kakotile tileset
Kakotile tileset contains the dates of the backup tiles overwritten in the past. The location and the format of the kakotile tileset are as the following:

## Kakotile location
If you have
```
{t}/{z}/{x}/{y}.{ext}
```
as the original tile, and
```
{t}/bak/{z}/{x}/{y}.{date}.{ext}
```
as the backup tile, the kokotile would be located at
```
{t}/kakotile/{z}/{x}/{y}.csv
```

## Kakotile format
Each kakotile contains comma-separated list of modification dates of the original tile.

For instance, if the content of the std/kakotile/15/29101/12903.csv is
```
20150606,20150522,20150129
```
, there must be 3 old versions of the original tile at std/15/29101/12903.png. And the old tiles would be located at:
```
std/bak/15/29101/12903.20150606.png
std/bak/15/29101/12903.20150522.png
std/bak/15/29101/12903.20150129.png
```

Please note that there would be 4 (not 3) versions of the tile because there is also original tile. The time-line of the each tile would be reconstructed from the modification time (mtime) of the current (original) tile and the dates stored in the kakotile.

## Kakotile generator
A reference implementation of kakotile generator is available at [kakotile-generator](https://github.com/gsi-cyberjapan/kakotile-generator/).
