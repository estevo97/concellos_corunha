# Parseo de robots.txt

Ao comprobar se Wikipedia permitía descargar a páxina dos municipios da Coruña mediante `RobotFileParser`, obtíñase inicialmente o resultado `False`.

O problema estaba na forma de descargar o ficheiro `robots.txt`. Ao utilizar o método `rp.read()`, a petición realizábase directamente co axente de usuario predeterminado de Python, que podía ser rexeitado polo servidor de Wikipedia.

Para solucionalo, utilizouse a biblioteca `requests` para descargar o ficheiro `robots.txt`, especificando un `User-Agent` propio:

```python
respuesta = requests.get(
    url_robots,
    headers={"User-Agent": "curso-sbd-demo/1.0"}
)
```

Despois, o contido descargado pasouse a `RobotFileParser` mediante o método `parse()`:

```python
rp = RobotFileParser()
rp.parse(respuesta.text.splitlines())
```

Deste xeito, `requests` encárgase de descargar o ficheiro e `RobotFileParser` de interpretar as súas regras e comprobar se está permitido acceder á páxina mediante `can_fetch()`.

Con esta modificación, a comprobación realizouse correctamente.