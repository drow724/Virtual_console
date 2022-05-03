<template>
      <template v-if="mode == 'WARN'">
        <p>{{currentTime}}
          <span class="yellow">&nbsp;{{mode}}</span>
          <span class="purple"> 6082 </span>
          ---
          <span>[nio-8080-exec-1]</span>
        </p>
      </template>
      <template v-if="mode == 'ERROR'">
        <p>{{currentTime}}
          <span class="red">{{mode}}</span>
          <span class="purple"> 6082 </span>
          ---
          <span>[nio-8080-exec-1]</span>
        </p>
      </template>
      <template v-if="mode == 'INFO'">
        <template v-if="msg == 'request'">
         <p>{{currentTime}}
            <span class="green">&nbsp;{{mode}}</span>
            <span class="purple"> 6082 </span>
            ---
            <span>[nio-8080-exec-1]</span>
            <span class="emerald">&nbsp;o.s.w.s.m.m.a.RequestMappingHandlerMapping&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</span>
            <span> : </span>
            <span >&nbsp;Mapped to public java.lang.String com.sangkon.log.LogApplication.getLogger()</span>
          </p>
          <p>{{currentTime}}
            <span class="green">&nbsp;{{mode}}</span>
            <span class="purple"> 6082 </span>
            ---
            <span>[nio-8080-exec-1]</span>
            <span class="emerald">&nbsp;o.s.w.s.m.m.a.RequestResponseBodyMethodProcessor</span>
            <span> : </span>
            <span >&nbsp;Using 'text/plain', given [*/*] and supported [text/plain, */*, text/plain, */*, application/json, application/*+json, application/json, application/*+json]</span>
          </p>
          <p>{{currentTime}}
            <span class="green">&nbsp;{{mode}}</span>
            <span class="purple"> 6082 </span>
            ---
            <span>[nio-8080-exec-1]</span>
            <span class="emerald">&nbsp;o.s.w.s.m.m.a.RequestResponseBodyMethodProcessor</span>
            <span> : </span>
            <span >&nbsp;Writing [log]</span>
          </p>
          <p>{{currentTime}}
            <span class="green">&nbsp;{{mode}}</span>
            <span class="purple"> 6082 </span>
            ---
            <span>[nio-8080-exec-1]</span>
            <span class="emerald">&nbsp;o.s.web.servlet.DispatcherServlet&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</span>
            <span> : </span>
            <span >&nbsp;Completed 200 OK</span>
          </p>
        </template>
        <template v-if="msg == 'query'">
          <p>{{currentTime}}
            <span class="green">&nbsp;{{mode}}</span>
            <span class="purple"> 6082 </span>
            ---
            <span>[nio-8080-exec-1]</span>
            <span class="emerald">&nbsp;o.a.c.c.C.[Tomcat].[nextome.com].[/{{request}}]&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</span>
            <span> : </span>
            <span >&nbsp;Open JPA EntityManager in OpenEntityManagerInViewInterceptor</span>
          </p>
          <p>{{currentTime}}
            <span class="green">&nbsp;{{mode}}</span>
            <span class="purple"> 6082 </span>
            ---
            <span>[nio-8080-exec-1]</span>
            <span class="emerald">&nbsp;{{bean}}&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</span>
            <span> : </span>
            <span>&nbsp;{{query}}</span>
          </p>
        </template>
      </template> 
</template>

<script>
export default {
  name: 'LineComponent',
    data() {
      return {
        currentTime: this.now(),
        mode: this.getMode(Math.floor(Math.random() * 99)),
        bean: this.getBean(),
        msg : this.getMsg(Math.floor(Math.random() * 2)),
        request : this.getRandom(),
        query : this.getQuery(Math.floor(Math.random() * 2))
      };
    },
    setup() {
     
    },
    created() {
     
    },
    mounted() {

    },
    unmounted() {
    
    },
    methods: {
      getMode(modeBranch) {

        let mode = '';

        if(modeBranch < 80){
          mode = 'INFO'
        } else if(modeBranch >= 80 && modeBranch < 90) {
          mode = 'WARN'
        } else {
          mode = 'ERROR'
        }

        return mode;
      },
      now() {

        let date = new Date();
        
        let year = date.getFullYear();
        let month = ('0' + (date.getMonth() + 1)).slice(-2);
        let day = ('0' + date.getDate()).slice(-2);

        let hours = ('0' + date.getHours()).slice(-2); 
        let minutes = ('0' + date.getMinutes()).slice(-2);
        let seconds = ('0' + date.getSeconds()).slice(-2); 

        let time = year + '-' + month  + '-' + day + ' ' + hours + ':' + minutes  + ':' + seconds;

        return time;
      },
      getBean() {

        let regExp = "ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz";

        let small = "abcdefghijklmnopqrstuvwxyz";
        let large = "ABCDEFGHIJKLMNOPQRSTUVWXYZ";

        let packages = '';

        for(var j = 0; j < 5; j++){
          packages += small.charAt(Math.floor(Math.random() * small.length));
        }

        let bean = '';

        for(var i = 0; i < 5; i++){
          if(i == 0){
            bean += large.charAt(Math.floor(Math.random() * large.length));
            continue;
          }
          bean += regExp.charAt(Math.floor(Math.random() * regExp.length));
        }

        let type = '';

        type = 'Repository';
        bean = "com."+packages+".repository."+bean+type;

        return bean;
      },
      getMsg(msgBranch){

        let msg = '';

        if(msgBranch == 0){
          msg = "query"
        } else {
          msg = "request"
        }

        return msg;
      },
      getQuery(queryBranch){

        let query = '';

        if(queryBranch == 0){

          query = "SELECT ";

          let max = Math.floor(Math.random() * 6)
          for(var i = 0; i < max; i++){
            query += this.getRandom()
            if(i == max-1){

               query += " ";
              continue;
            }
            query += ", "
          } 

          query += "FROM " + this.getRandom();
          
          query += " WHERE 1=1 ";

          query += this.getWhere();

        } else if(queryBranch == 1) {

          query = "UPDATE ";

          let max = Math.floor(Math.random() * 6);

          for(i = 0; i < max; i++){

            query += this.getRandom()

            if(i == max-1){

              query += " ";

              continue;
            }

            query += ", "
          }

          query += "FROM " + this.getRandom();
          query += " WHERE 1=1 ";
          query += this.getWhere();

        } else {

          query = "DELETE " + this.getRandom() + "FROM" + this.getRandom() + " WHERE 1=1 "

          query += this.getWhere();
        }

        return query;
      },
      getWhere(){

        let where = '';

        for(var i = 0; i < Math.floor(Math.random() * 15); i++){
          where += "AND " + this.getRandom() + " = \"" + this.getRandom() + "\" ";
        }

        return where;
      },
      getRandom(){
        let random = '';

        let large = "ABCDEFGHIJKLMNOPQRSTUVWXYZ";

        for(var n = 0; n < 5; n++){
          random += large.charAt(Math.floor(Math.random() * large.length));
        }

        return random;
      }
    }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

p {
  color: white;
}

.red {
  color: red;
}

.yellow {
  color: yellow;
}

.green {
  color: lightgreen;
}

.purple {
  color: purple;
}

.emerald {
  color: #008080;
}

</style>
