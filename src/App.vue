<template>

    <div id="formulario" class="grid w-full m-auto mt-4">

        <div class="col-8">

            <div class="field">
                <label for="nome">Valor do Empréstimo<sup class="text-pink-500 text-lg">*</sup></label>
                <InputNumber
                    v-model="emprestimo"
                    mode="currency"
                    currency="BRL"
                    placeholder="R$ 100.000,00"
                    class="w-full"
                    locale="pt-BR"
                />
            </div>

            <div class="field">
                <label for="nome">Valor do Imóvel <sup class="text-pink-500 text-lg">*</sup></label>
                <InputNumber
                    v-model="imovel"
                    mode="currency"
                    currency="BRL"
                    placeholder="R$ 700.000,00"
                    class="w-full"
                    locale="pt-BR"
                />
            </div>

            <div class="field">
                <label for="nome">Quantidade de meses</label>
                <Slider v-model="qtdMeses" :max="120" />
            </div>

            <div>
                <Button label="Simular Empréstimo" />
            </div>

        </div>

        <div class="col-4">

            <div class="bg-white text-xl text-center p-6" id="infoParcela">

                <div>Valor da parcela:</div>

                <div id="total" class="text-3xl mt-1">R$ 1.989,00</div>

                <p class="text-lg mt-8">Prazo para pagamento:</p>

                <p class="text-lg font-bold">Amortização: TABELA PRICE</p>

                <p class="text-justify text-lg text-600 ">
                    A taxa de juros varia a partir de 0.99% ao mês, dependendo do tipo de
                    imóvel. A parcela apresentada já inclui os custos aproximados com
                    avaliação do imóvel, seguros e custos cartoriais.
                </p>

            </div>

        </div>

    </div>
    
</template> 

<script>
export default {
  name: "App",
  data() {
    return {
      emprestimo: "",
      imovel: "",
      qtdMeses: "",
      parcela: "",
    }
  }
}
</script>

<style lang="css" scoped>

    #formulario {
        max-width: 900px;
        --border-radius: 5px;
    }

    #total {
        border-bottom: 1px solid rgb(190 185 185);
        
    }

    #infoParcela{
        border: 1px solid #ced4da;
    }

</style>
