// Cria a variavel para registrar o primerio ID do banco 

UpdateContext({loading:true});;

Clear(JsonTratado);;
UpdateContext({VarPrimeiroJson:First(dataset).ID});;

// Cria a variavel para registrar o ultimo ID do banco 

UpdateContext({VarUltimoJson:First(Sort(dataset;ID;SortOrder.Descending)).ID});;

//Cria varial com a qtd de vezes que o loop para coletar vai rodar

UpdateContext({VarQtdRepeticoesJson:Sequence(RoundUp((VarUltimoJson-VarPrimeiroJson)/2000;0)+1)});;

// iniciar o loop que busca todos os itens no Sharepoint
ForAll(
    VarQtdRepeticoesJson As Repeticao;

    With(
        {
            valor_anterior: Value(Repeticao.Value) * 2000;
            valor_proximo: (Value(Repeticao.Value) + 1) * 2000
        };

        If(
            VarUltimoJson > valor_anterior;
            Collect(
                ColJson;
                ShowColumns(
                    Filter(dataset;ID_ESPELHO>valor_anterior&&ID_ESPELHO<=valor_proximo);
                    json
                )
            )
        )
    )
);;



Clear(JsonTratado);;
// faço o loop com a collect de todos os dados do banco , e dentro da collect faço outro loop para cada linha acessando a cedula e desmembrando o json

ForAll(
    dataset As JSON_entrada;

    Collect(
        JsonTratado;

        ForAll(
            ParseJSON(JSON_entrada.json);

           {
                Compania: ThisRecord.'Company Name';
                ModelName: ThisRecord.'Model Name';
                MobileWeight: ThisRecord.'Mobile Weight';
                RAM: ThisRecord.'RAM';
                FrontCamera: ThisRecord.'Front Camera';
                BackCamera: ThisRecord.'Back Camera';
                Processor: ThisRecord.'Processor';
                BatteryCapacity: ThisRecord.'Battery Capacity';
                ScreenSize: ThisRecord.'Screen Size';
                LaunchedPricePakistan: ThisRecord.'Launched Price (Pakistan)';
                LaunchedPriceIndia: ThisRecord.'Launched Price (India)';
                LaunchedPriceChina: ThisRecord.'Launched Price (China)';
                LaunchedPriceUSA: ThisRecord.'Launched Price (USA)';
                LaunchedPriceDubai: ThisRecord.'Launched Price (Dubai)';
                LaunchedYear: ThisRecord.'Launched Year';
                VALOR: ThisRecord.'VALOR'
                }
        )
    )
)

;;

UpdateContext({loading:false});;
