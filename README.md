export const salvarPushToken = async (req, res) => {
    try {
        const id_user = req.user.id; // Pega o ID do usuário logado através do token JWT
        const { push_token } = req.body; // Pega o token do celular enviado pelo Front

        if (!push_token) {
            return res.status(400).json({ message: 'Push token não fornecido.' });
        }

        // Salva o token do celular diretamente na linha do usuário dono dele
        await db.query(
            'UPDATE usuario SET push_token = ? WHERE id_user = ?',
            [push_token, id_user]
        );

        res.json({ message: 'Token de notificação salvo com sucesso!' });
    } catch (err) {
        console.error("Erro ao salvar push token:", err);
        res.status(500).json({ message: 'Erro interno ao salvar token.' });
    }
};
