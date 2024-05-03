<p align="center">
  <img width="500" src="https://user-images.githubusercontent.com/10407788/204477834-2533241a-5927-4f56-959e-4e8494027bc0.png"/>
  <p align="center">Simple and Fast Geospatial OGC Features and Tiles API for PostGIS.</p>
</p>
<p align="center">
  <a href="https://github.com/developmentseed/tipg/actions?query=workflow%3ACI" target="_blank">
      <img src="https://github.com/developmentseed/tipg/workflows/CI/badge.svg" alt="Test">
  </a>
  <a href="https://codecov.io/gh/developmentseed/tipg" target="_blank">
      <img src="https://codecov.io/gh/developmentseed/tipg/branch/main/graph/badge.svg" alt="Coverage">
  </a>
  <a href="https://pypi.org/project/tipg" target="_blank">
      <img src="https://img.shields.io/pypi/v/tipg?color=%2334D058&label=pypi%20package" alt="Package version">
  </a>
  <a href="https://github.com/developmentseed/tipg/blob/main/LICENSE" target="_blank">
      <img src="https://img.shields.io/github/license/developmentseed/tipg.svg" alt="License">
  </a>
</p>

---

**Documentation**: <a href="https://developmentseed.org/tipg/" target="_blank">https://developmentseed.org/tipg/</a>

**Source Code**: <a href="https://github.com/developmentseed/tipg" target="_blank">https://github.com/developmentseed/tipg</a>

---

`tipg`, pronounced *T[ee]pg*, is a **Python** package that helps create lightweight OGC **Features** and **Tiles** API with a PostGIS Database backend. The API has been designed for [OGC Features](https://ogcapi.ogc.org/features) and [OGC Tiles](https://ogcapi.ogc.org/tiles/) specifications.

> **Note**
> This project is the result of the merge between [tifeatures](https://github.com/developmentseed/tifeatures) and [timvt](https://github.com/developmentseed/timvt).

## Deploy to local
```bash
$ docker build -t tipg-uvicorn:latest -f dockerfiles/Dockerfile.custom .
$ docker run -d -p 8080:8080 --name tipg-uvicorn -e DATABASE_URL=postgresql://postgres:postgres@localhost:5432/postgres tipg-uvicorn:latest
```

**p.s.** 
You can also use `-e DATABASE_URL=postgressql://postgres:postgres@localhost:5432/postgres` to connect to a local database or If you can see the other schema, you can use `-e TIPG_DB_SCHEMAS='["public, "other_schema"]'` to specify the schema.

## Deploy image to ECR
```bash
$ aws ecr get-login-password --region us-east-1 | docker login --username AWS --password-stdin 123456789012.dkr.ecr.ap-southeast-1.amazonaws.com
$ docker build -t tipg-uvicorn:latest -f dockerfiles/Dockerfile.custom .
$ docker tag tipg:latest 123456789012.dkr.ecr.ap-southeast-1.amazonaws.com/tipg:latest
$ docker push 123456789012.dkr.ecr.ap-southeast-1.amazonaws.com/tipg:latest
```

## Deploy to ECS
```bash
$ aws ecs update-service --cluster tipg --service tipg --force-new-deployment
```
