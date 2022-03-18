<template>
  <div id="formulario" class="grid w-full m-auto mt-4">
    <div class="col-8">
      <div class="field">
        <label for="nome"
          >Valor do Empréstimo<sup class="text-pink-500 text-lg">*</sup></label
        >
        <InputNumber
          v-model="emprestimo"
          mode="currency"
          currency="BRL"
          placeholder="R$ 100.000,00"
          :class="camposErros.indexOf('emprestimo')!=-1?'w-full p-invalid':'w-full'"
          locale="pt-BR"
        />
      </div>

      <div class="field">
        <label for="nome"
          >Valor do Imóvel <sup class="text-pink-500 text-lg">*</sup></label
        >
        <InputNumber
          v-model="imovel"
          mode="currency"
          currency="BRL"
          placeholder="R$ 700.000,00"
          :class="camposErros.indexOf('imovel')!=-1?'w-full p-invalid':'w-full'"
          locale="pt-BR"
        />
      </div>

      <div class="field">
        <label for="nome">Quantidade de meses</label>
        <Slider class="mt-3 ml-2" v-model="qtdMeses" :min="1" :max="120" />
      </div>

      <div class="mt-8">
        <Button
          class="bg-indigo-600 border-indigo-600"
          label="Simular Empréstimo"
          @click="calculo"
        />
      </div>
    </div>

    <div class="col-4">
      <div class="bg-white text-xl text-center p-5" id="infoParcela">
        <div>Valor da parcela:</div>

        <div id="total" class="text-3xl mt-1">
          {{
            new Intl.NumberFormat("pt-BR", {
              style: "currency",
              currency: "BRL",
            }).format(total)
          }}
        </div>

        <p class="text-lg mt-4">Prazo para pagamento:</p>

        <div>
          {{ qtdMeses }} Meses
        </div>

        <p class="text-lg font-bold mt-6">Amortização: TABELA PRICE</p>

        <p class="text-justify text-base text-600 my-4">
          A taxa de juros varia a partir de 0.99% ao mês, dependendo do tipo de
          imóvel. A parcela apresentada já inclui os custos aproximados com
          avaliação do imóvel, seguros e custos cartoriais.
        </p>
      </div>
    </div>
  </div>
  <Toast position="top-right" />
</template> 

<script>
export default {
  name: "App",
  data() {
    return {
      emprestimo: 0,
      imovel: 0,
      qtdMeses: 48,
      total: 0,
      camposErros: [],
    };
  },

  methods: {
    calculo: function () {
      this.camposErros = [];

      if (this.emprestimo <= 0) this.camposErros.push("emprestimo");

      if (this.imovel <= 0) this.camposErros.push("imovel");

      if (this.camposErros.length > 0) {
        this.$toast.add({
          severity: "error",
          summary: "Informações Inválidas",
          detail: "Preencha corretamente todas as informações!",
          life: 3000,
        });
      }
      
      else {
        if (this.imovel <= 100000) {
          this.total = (this.emprestimo / this.qtdMeses) * 1.01;
        } else if (this.imovel > 1000000) {
          this.total = (this.emprestimo / this.qtdMeses) * 1.015;
        } else {
          // TODO Verificar as outras taxas
          this.total = -1;
        }
      }
    },
  },
};
</script>

<style lang="scss" scoped>
#formulario {
  max-width: 900px;
}

#total {
  border-bottom: 1px solid rgb(190 185 185);
}

#infoParcela {
  border: 1px solid #ced4da;
  border-radius: 10px;
}
</style>
