from pathlib import Path
import shutil

# Caminho base para o projeto
project_name = "tempo-espera-app"
base_path = Path("/mnt/data") / project_name

# Estrutura de diretórios
src_path = base_path / "src"
components_path = src_path / "components" / "ui"
components_path.mkdir(parents=True, exist_ok=True)

# Arquivo principal do componente React
app_code = """
import React, { useState, useEffect } from 'react';
import { Card, CardContent } from "@/components/ui/card";
import { Input } from "@/components/ui/input";
import { Button } from "@/components/ui/button";
import { Table, TableHeader, TableRow, TableCell, TableBody } from "@/components/ui/table";

const TempoEsperaApp = () => {
  const [dados, setDados] = useState([]);
  const [motorista, setMotorista] = useState("");
  const [transportadora, setTransportadora] = useState("");
  const [tipo, setTipo] = useState("EXPEDIÇÃO");
  const [status, setStatus] = useState("PATIO");

  const handleCheckIn = () => {
    setDados([
      ...dados,
      {
        motorista,
        transportadora,
        tipo,
        status,
        checkin: new Date(),
        checkout: null,
      },
    ]);
    setMotorista("");
    setTransportadora("");
  };

  const handleCheckout = (index) => {
    const novosDados = [...dados];
    novosDados[index].checkout = new Date();
    novosDados[index].status = "LIBERADO";
    setDados(novosDados);
  };

  const calcularTempo = (checkin, checkout) => {
    const fim = checkout ? new Date(checkout) : new Date();
    const diff = Math.abs(fim - new Date(checkin));
    const horas = Math.floor(diff / 3600000);
    const minutos = Math.floor((diff % 3600000) / 60000);
    const segundos = Math.floor((diff % 60000) / 1000);
    return `${horas.toString().padStart(2, '0')}:${minutos
      .toString()
      .padStart(2, '0')}:${segundos.toString().padStart(2, '0')}`;
  };

       const temposEspera = dados.map(d => calcularTempo(d.checkin, d.checkout));     
    const maiorTempo = temposEspera.sort().reverse()  [0];
  const mediaTempo = () => {
    if (dados.length === 0) return "00:00:00";
    const totalMs = dados.reduce((acc, cur) => {
      const fim = cur.checkout ? new Date(cur.checkout) : new Date();
      return acc + (fim - new Date(cur.checkin));
    }, 0);
    const avg = totalMs / dados.length;
    const horas = Math.floor(avg / 3600000);
    const minutos = Math.floor((avg % 3600000) / 60000);
    const segundos = Math.floor((avg % 60000) / 1000);
    return `${horas.toString().padStart(2, '0')}:${minutos
      .toString()
      .padStart(2, '0')}:${segundos.toString().padStart(2, '0')}`;
  };

  return (
    <div className="p-6 space-y-6">
      <div className="grid grid-cols-3 gap-4">
        <Card className="bg-red-500 text-white">
          <CardContent className="text-center">
            <h2 className="text-xl">MAIOR TEMPO DE ESPERA</h2>
            <p className="text-2xl font-bold">{maiorTempo || "00:00:00"}</p>
          </CardContent>
        </Card>
        <Card className="bg-green-600 text-white">
          <CardContent className="text-center">
            <h2 className="text-xl">MÉDIA DE ESPERA</h2>
            <p className="text-2xl font-bold">{mediaTempo()}</p>
          </CardContent>
        </Card>
        <Card className="bg-purple-600 text-white">
          <CardContent className="text-center">
            <h2 className="text-xl">CAMINHÕES NO PÁTIO</h2>
            <p className="text-2xl font-bold">{dados.filter(d => d.status === "PATIO").length}</p>
          </CardContent>
        </Card>
      </div>

      <div className="grid grid-cols-4 gap-4">
        <Input placeholder="Motorista" value={motorista} onChange={(e) => setMotorista(e.target.value)} />
        <Input placeholder="Transportadora" value={transportadora} onChange={(e) => setTransportadora(e.target.value)} />
        <Button onClick={handleCheckIn}>Check-in</Button>
      </div>

      <Table>
        <TableHeader>
          <TableRow>
             <TableCell>Motorista</TableCell> 
             <TableCell>Transportadora</TableCell> 
            <TableCell>Status</TableCell>
            <TableCell>Check-in</TableCell>
            <TableCell>Check-out</TableCell>
             <TableCell>Tempo de Espera</TableCell> 
             <TableCell>Ação</TableCell> 
          </TableRow>
        </TableHeader>
        <TableBody>
            {dados.map((item, index) => (  
            <TableRow key={index}>
                <TableCell>{item.motorista}</TableCell>  
                <TableCell>{item.transportadora}</TableCell>  
              <TableCell>{item.status}</TableCell>
              <TableCell>{new Date(item.checkin).toLocaleString()}</TableCell>
                 <TableCell>{item.checkout ? new Date(item.checkout).toLocaleString() : "-"}</TableCell>   
   do caminho de importação Pathlib             <TableCell>{calcularTempo(item.checkin, item.checkout)}</TableCell>
Importação Shutil<TableCell>
                {!item.checkout && (
#    Caminho base para o projeto              <Button onClick={() => handleCheckout(index)}>Finalizar  </Button>
Project_Name = "tempo-espera-app"            )}
base_path = Caminho("/mnt/dados") / project_name</TableCell>
            </TableRow>
#    Estrutura de diretórios      ))}  
src_path = base_path / "src"    </TableBody>
Componentes_Path = src_Path / "Componentes" / "UI"</Table>
componentes_path.mkdir(pais=Verdadeiro, exist_ok=Verdadeiro)</div>
  );
#    Arquivo principal do componente React  

importar React, { useState, useEffect } de 'react';
importação {Cartão, Conteúdo do Cartão } de "@/componentes/ui/cartão";

#       Escreve o arquivo     
importação { Tabela, Cabeçalho de Tabela, TableRow, TableCell, TableBody } de "@/componentes/ui/tabela";
app_file.write_text(app_code)

#  Compacta tudo em um ZIP
   const [motorista, setMotorista] = useState(""); 
 const [transportadora, setTransportadora] = useState(""); 

zip_path.name  # Nome do arquivo gerado para download[status, setStatus] = useState("PATIO"); 
