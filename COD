import streamlit as st
import pandas as pd
from io import BytesIO

st.set_page_config(page_title="CSV → Parquet", layout="centered")
st.title("📂 Convertidor de CSV a Parquet")

# Subir hasta 4 archivos CSV
archivos = st.file_uploader("Sube tus archivos CSV (máximo 4)", type=["csv"], accept_multiple_files=True)

if archivos:
    if len(archivos) > 4:
        st.warning("⚠️ Solo se procesarán los primeros 4 archivos.")
        archivos = archivos[:4]

    for archivo in archivos:
        try:
            df = pd.read_csv(archivo)
            buffer = BytesIO()
            df.to_parquet(buffer, index=False)
            buffer.seek(0)

            nombre_salida = archivo.name.replace(".csv", ".parquet")

            st.download_button(
                label=f"⬇️ Descargar {nombre_salida}",
                data=buffer,
                file_name=nombre_salida,
                mime="application/octet-stream"
            )
        except Exception as e:
            st.error(f"Error al procesar {archivo.name}: {e}")
