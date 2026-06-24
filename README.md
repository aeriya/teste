// utils/src/notifications.js

import axios from 'axios';

export const enviarNotificacao = async (tokenDoCelular, titulo, mensagem) => {
    // Se o usuário não tiver um celular cadastrado (token nulo), ignora
    if (!tokenDoCelular) return;

    try {
        // Faz uma requisição POST direta para os servidores da Expo
        await axios.post('https://exp.host/--/api/v2/push/send', {
            to: tokenDoCelular,
            sound: 'default', // Ativa o som padrão de notificação no celular
            title: titulo,
            body: mensagem
        });
        console.log("Notificação enviada com sucesso!");
    } catch (error) {
        console.error("Erro ao mandar a ordem para a Expo:", error.message);
    }
};
